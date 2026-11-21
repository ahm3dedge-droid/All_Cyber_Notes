**Description:**

The Skeleton key attack is a persistence method in which we inject a master password in LSA → LSASS process memory for each Authentication user in the domain Controller, LSA contains local data of passwords in memory, Restarting the Domain Controller can loose This password and we no longer able to Authenticate with this master Password or also called Skeleton Key. This created a New Master Password as “mimikatz”.

**What is LSASS and LSA?**

Lsass.exe is a process which holds all the Password hashes in the memory to provide Authentication Services, in this instance this process is running on the domain controller and we are injecting the Skeleton key in the process with domain Admin Rights.

**Requirements:**

🔸️We must have the domain admin privileges to perform this action.

🔸️command must be executed on to the domain controller to inject skeleton key into the LSASS process

**Key Points:**

🔸️Mimikatz Tools is used to perform this attack.

🔸️After Restarting Domain Controller we are not able to use this skeleton key because when we restart the domain controller all the data will be wiped and removed from the Random Access Memory.

🔸️We can only Create This Skeleton Key 1 time because after this we need to restart the Domain Controller to set another time Master Password. there is only 1 place for master password in the Domain Controller memory

**Performing Attack:**

We can Use this command to Create a Skeleton Key

`Invoke-Mimikatz -Command ‘"privilege::debug" “misc::skeleton”’ -ComputerName dc02.universe.com`

![[Pasted image 20251221101834.png]]

**Checking our newly set skeleton key:**

we can login to any user or machine account with a new skeleton key “mimikatz”

`runas /user:multiverse\ahmed powershell.exe`

Enter Password: "_mimikatz_"

![[Pasted image 20251221101841.png]]