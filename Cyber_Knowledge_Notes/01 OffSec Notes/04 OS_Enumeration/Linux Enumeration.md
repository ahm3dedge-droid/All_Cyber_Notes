To Get the information about the operating System

`cat` `/etc/os-release`

`cat /etc/*-release`

![[Pasted image 20251219211414.png]]

Get the hostname of the machine

![[Pasted image 20251219211425.png]]

Look for valuable information if these files

`cat /etc/passwd`

`cat /etc/groups`

`cat /etc/shadow` _(root permissions needed to view this)_

![file://C:/Users/ahmed/AppData/Local/Temp/.Y0WYH3/3.png](file://C:/Users/ahmed/AppData/Local/Temp/.Y0WYH3/3.png)

To find the installed applications you can consider listing the files in `/usr/bin/` and `/sbin/`:

- `ls -lh /usr/bin/`
- `ls -lh /sbin/`

![[Pasted image 20251219211438.png]]

**List installed Packages**

RMP Based

`rpm -qa`

Debian Based

`dpkg -l`

![[Pasted image 20251219211444.png]]

Files such as `/etc/passwd` reveal the usernames; 

![[Pasted image 20251219211449.png]]

You can show who is logged in using `who`.

![[Pasted image 20251219211459.png]]

use `w`, which shows who is logged in and what they are doing.

![[Pasted image 20251219211504.png]]

To print the real and effective user and group IDS, you can issue the command `id` (for ID).

![[Pasted image 20251219211515.png]]

`last` displays a listing of the last logged-in users

![[Pasted image 20251219211521.png]]

lists the allowed command for the invoking user on the current system.

`sudo -l` 

List Nework Details with this command

`ip a s`

`ip address show`

![[Pasted image 20251219211526.png]]

The DNS servers can be found in the `/etc/resolv.conf`

`cat /etc/resolve.conf`

![[Pasted image 20251219211530.png]]

Netstat

![[Pasted image 20251219211534.png]]

Display the Process ID and Names of all the Listening Connections

`sudo netstat -plt`

![[Pasted image 20251219211538.png]]

show _All TCP and_ _UDP_ listening and established connections and the _program_ names with addresses and ports in _numeric_ format.

`netstat -atupn` 

![[Pasted image 20251219211544.png]]

display only Internet and network connections

`lsof -i`

`sudo lsof -i`

![[Pasted image 20251219211550.png]]

List only for Port 25

`lsof -i :25`

![[Pasted image 20251219211556.png]]

List all the processes

`ps axjf` 

`ps -ef`

![[Pasted image 20251219211600.png]]

________________________________________________________________________________________________________________

# ALL LINUX COMMANDS

(_SCREENSHOT FROM TRYHACKME_)

![[Pasted image 20251219211605.png]]

________________________________________________________________________________________________________________