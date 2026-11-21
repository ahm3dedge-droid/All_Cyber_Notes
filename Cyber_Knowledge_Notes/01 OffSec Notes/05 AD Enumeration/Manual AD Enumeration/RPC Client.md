connect to the Domain Controller over RPC
```
rpcclient -U chloe.stevens%Sheba12006 10.200.71.101
```

> we supplied user and password like this: `username`%`password`
---
### RPC Client Commands
- Domain Information Query
```
querydominfo
```

- Enumerate Domain Users
```
enumdomusers
```

- Enumerating Domain Groups
```
enumdomgroups
```

- Query specific Group information with RID of group
```
querygroup {RID_HERE}
```

- query a specific user 
```
queryuser {USERNAME_HERE}
```

- Enumerate Privileges
```
enumprivs
```

- Get domain password information
```
getdompwinfo
```

- Get the User domain Password information
```
getusrdompwinfo {RID_HERE}
```

- Enumerating SID from LSA
```
lsaenumsid
```

- Creating Domain User
```
createdomuser {USERNAME} 
setuserinfo2 {USERNAME} 24 {PASSWORD} 
enumdomusers
```
---
- check user's SID with this lookup command
```
lookupnames {USERNAME_HERE}
```

- 