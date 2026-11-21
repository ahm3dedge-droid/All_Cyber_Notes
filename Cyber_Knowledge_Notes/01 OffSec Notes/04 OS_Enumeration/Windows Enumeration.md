detailed information about the system, such as its build number and installed patches

`systeminfo`

![[Pasted image 20251219211811.png]]

check installed updates using

`wmic qfe get Caption,Description`

![[Pasted image 20251219211817.png]]

check the installed and started Windows services

`net start`

![[Pasted image 20251219211822.png]]

See installed apps

`wmic product get name, version, vendor`

![[Pasted image 20251219211830.png]]

Get Details about Users and Privileges

`whoami`

`whoami /priv`

![[Pasted image 20251219211836.png]]

use `whoami /groups` to know which groups you belong to

![[Pasted image 20251219211844.png]]

You can view users by running `net user`.

![[Pasted image 20251219211850.png]]

discover the available groups using `net group` if the system is a Windows Domain Controller or `net localgroup` otherwise

![[Pasted image 20251219211855.png]]

You can list the users that belong to the local administratorsâ€™ group using the commandÂ `net localgroup administrators`.

![[Pasted image 20251219211908.png]]

Use `net accounts` to see the local settings on a machine; moreover, you can use `net accounts /domain` if the machine belongs to a domain. This command helps learn about password policy, such as minimum password length, maximum password age, and lockout duration.

see network basic details

### `ipconfig /all`

![[Pasted image 20251219211914.png]]

Display the details of listening and established connections on the machine

### `netstat -abno`

`-a` to display all listening ports and active connection
`-b`  lets us find the binary involved in the connection
`-n`  is used to avoid resolving IP addresses and port numbers
`-o`  display the process ID (PID)

![[Pasted image 20251219211923.png]]

`arp -a`

![[Pasted image 20251219212004.png]]

list the shares are available on current windows machine

`net share`

________________________________________________________________________________________________________________

# ALL WINDOWS COMMANDS

(_SCREENSHOT FROM TRYHACKME_)

![[Pasted image 20251219212009.png]]

________________________________________________________________________________________________________________