
This is the list of services which can be abused using constrained delegation,
also lists the tools can be used to abuse it attack  

| **Service (SPN)** | **Attack Vector**      | **Access / Impact**                             | **Common Tools Used**           |
| ----------------- | ---------------------- | ----------------------------------------------- | ------------------------------- |
| **CIFS**          | S4U → TGS request      | SMB access, file read/write, share access       | Rubeus, smbclient, CrackMapExec |
| **HTTP**          | `/altservice:HTTP`     | WinRM / web services → remote command execution | Rubeus, Evil-WinRM              |
| **HOST**          | `/altservice:HOST`     | PsExec / SCM → SYSTEM shell                     | Rubeus, PsExec, Impacket        |
| **LDAP**          | `/altservice:LDAP`     | **DCSync**, AD object abuse                     | Rubeus, Mimikatz, Impacket      |
| **MSSQLSvc**      | `/altservice:MSSQLSvc` | SQL Server → DB admin, data dump                | Rubeus, SQLCMD, Impacket        |
| **RPCSS**         | `/altservice:RPCSS`    | Service abuse, lateral movement                 | Rubeus, Impacket                |
| **WSMAN**         | `/altservice:WSMAN`    | WinRM → PowerShell remoting                     | Rubeus, Evil-WinRM              |
| **TERMSRV**       | `/altservice:TERMSRV`  | RDP access                                      | Rubeus, xfreerdp                |
| **DNS**           | `/altservice:DNS`      | DNS abuse / enumeration                         | Rubeus, dnscmd                  |
| **TIME**          | `/altservice:TIME`     | Low impact / rarely abused                      | Rubeus                          |
