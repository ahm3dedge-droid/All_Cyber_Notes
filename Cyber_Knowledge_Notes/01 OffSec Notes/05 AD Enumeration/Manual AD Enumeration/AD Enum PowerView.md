# **PowerView**
## Domain Computers Enumeration
List all computers in current Domain:
```
Get-DomainComputer | Select Name,Description | Sort Name
```


Get Computer objects that have Unconstrained Delegation:
```
Get-DomainComputer -Unconstrained
```
---
## Domain Enumeration
Domain Information:
```
Get-NetDomain
```

Get Domain SID
```
Get-DomainSID
```
---
## Domain Controller Enumeration
Get all Domain Controllers:
```
Get-NetDomainController
```

Get Primary Domain Controller:
```
Get-NetDomain | Select-Object 'PdcRoleOwner'
```

Get Domain Controller in different Domain:
```
Get-NetDomainController -Domain <Domain>
```

---
## Domain Policy Information:
```
Get-DomainPolicy
```
```
(Get-DomainPolicy)."SystemAccess"
```
```
(Get-DomainPolicy –domain <Domain>)."systemaccess"
```
```
(Get-DomainPolicy)."KerberosPolicy" 
```

---
## Domain Trust Enumeration
Enumerate all Domains in the forest
```
Get-NetForestDomain
```

Get all Domains in Forest then list each Domain trust
```
Get-NetForestDomain -Verbose | Get-DomainTrust
```

Map all reachable Domain trusts
```
Get-DomainTrustMapping
```
```
Get-DomainTrustMapping | Select SourceName,TargetName,TrustType,TrustDirection
```

List external trusts
```
Get-NetForestDomain -Verbose | Get-DomainTrust |?{$_.TrustType -eq 'External'}
```

Enumerate trusts across the domain
```
Get-DomainTrust
```

Find users in the current Domain that reside in Groups across trusts
```
Find-ForeignUser
```
---
## Forest Enumeration
Get details about current Forest
```
Get-NetForest
```
```
Get-NetForest -Forest <Forest>
```

Get all Domains in current Forest
```
Get-NetForestDomain
```
```
Get-NetForestDomain -Forest <Forest>
```

Get global catalogs in current Forest
```
Get-NetForestCatalog
``````
```
Get-NetForestCatalog -Forest <Forest>
```

Map Forest trusts
```
Get-NetForestTrust
```
```
Get-NetForestTrust -Forest <Forest>
```
---
## Group Enumeration
List all Groups in current Domain
```
Get-NetGroup
```
```
Get-NetGroup -Properties SamAccountName | Sort SamAccountName
```

List all Groups in alternative Domain
```
Get-NetGroup -Domain <Domain>
```

Search for Groups with partial wildcard
```
Get-NetGroup "*admin*"
```
```
Get-NetGroup "*admin*"-Properties SamAccountName | Sort SamAccountName
```

List all local groups on Domain system
```
Get-NetLocalGroup -ComputerName <Hostname>
```

Identify interesting groups on a Domain Controller
```
Get-NetDomainController | Get-NetLocalGroup
```

Get all domain controllers then get each group and list members  
```
Get-NetDomainController | Get-NetLocalGroup | Select -ExpandProperty GroupName | Get-NetGroupMember | Select GroupName,MemberName | Sort GroupName
```

Get All groups and members of groups
```
Get-NetGroup | Get-NetGroupMember | Select GroupName,MemberName | Sort GroupName
```

List Groups of which a user is a member of (Recursive)
```
Get-DomainGroup -MemberIdentity "<User>"
```
```
Get-DomainGroup -MemberIdentity "<Group>"
```
---
Convert From SID to Object Name
```
ConvertFrom-SID S-1-5-21-3330634377-1326264276-632209373-113
```

---

Get all OU's in Domain
```
Get-DomainOU
```
```
Get-DomainOU -Domain <Domain>
```
```
Get-DomainOU -Properties OU,DistinguishedName | Sort OU
```
---
## User Enumeration
List all user accounts in Domain
```
Get-DomainUser
```

List enabled user accounts
```
Get-DomainUser -UACFilter NOT_ACCOUNTDISABLE -Properties Name,SamAccountName,Description | Sort Name
```
```
Get-DomainUser -UACFilter NOT_ACCOUNTDISABLE -Properties Name,Description,pwdlastset,badpwdcount | Sort Name
```

List specific user account
```
Get-DomainUser -Username <Username>
```

Getcurrently logged on users from selected system
```
Get-NetLoggedon -ComputerName <Hostname>
```

Get last logged user on a remote computer (Requires admin and remote registry)
```
Get-LastLoggedOn -ComputerName <Hostname>
```

**Get kerberoastable users**
```
Get-DomainUser -SPN | select Name,SrvicepPincipalnNme
```

**Get AS-REP roastable users**
```
Get-DomainUser -PreauthNotRequired | select Name
```

Search for string in User Description field
```
Get-DomainUser -Properties samaccountname,description | Where {$_.description -ne $null}
```

Search for string in userPassword field
```
Get-DomainUser -Properties userPassword | Where {$_.userPassword -ne $null}
```

Search for string in unixUserPassword field
```
Get-DomainUser -Properties unixUserPassword | Where {$_.unixUserPassword -ne $null}
```
---
## Share Enumeration

Find shared on hosts in the current domain
```
Invoke-ShareFinder -Verbose
```
```
Invoke-ShareFinder -ExcludeStandard -ExcludePrint -ExcludeIPC
```

Find sensitive files on computers in the domain
```
Invoke-FileFinder -Verbose
```

Get all fileservers of the domain
```
Get-NetFileServer
```

---
## (GPO) Group Policy Object Enumeration

Get list of GPO's in the current domain
```
Get-NetGPO
```
```
Get-NetGPO -Computername <computername>
```

Get GPO's which uses restricteds groups or groups.xml for interesting users
```
Get-NetGPOGroup
```

Get users which are in a local group of a machine using GPO
```
Find-GPOComputerAdmin -Computername <computername>
```

Get machines where the given user is member of a specific group
```
Find-GPOLocation -Username student244 -Verbose
```

Get OU's in a domain
```
Get-NetOU -Fulldata
```

Get machines that are part of an OU
```
Get-NetOU StudentMachines | %{Get-NetComputer -ADSPath $_}
```

Get GPO applied on an OU
```
gplink from Get-NetOU -Fulldata
```

```
Get-NetGPO -GPOname "{<gplink>}"
```

---
## Powerview ACL 
Get the ACL's associated with the specified object
```
Get-ObjectACL -SamAccountName <accountname> -ResolveGUIDS
```

Get the ACL's associated with the specified prefix to be used for search
```
Get-ObjectACL -ADSprefix ‘CN=Administrator,CN=Users’ -Verbose
```

Get the ACL's associated with the specified path
```
Get-PathAcl -Path \\<Domain controller>\sysvol
```

Search for interesting ACL's
```
Invoke-ACLScanner -ResolveGUIDs
```
```
Invoke-ACLScanner -ResolveGUIDs | select IdentityReference, ObjectDN, ActiveDirectoryRights | fl
```

Search of interesting ACL's for the current user
```
Invoke-ACLScanner | Where-Object {$_.IdentityReference –eq [System.Security.Principal.WindowsIdentity]::GetCurrent().Name}
```

---
