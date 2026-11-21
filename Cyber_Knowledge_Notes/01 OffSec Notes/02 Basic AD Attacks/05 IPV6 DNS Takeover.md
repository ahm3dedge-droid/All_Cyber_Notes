# **IPv6 DNS Takeover**

in this attack, we as an attacker “ the attacker acts as an IPv6 router responding to configuration request from our victim and assign it with an IPv6 address and an IPv6 DNS server. ” basically act as a IPv6 DHCP Server and provide IPv6 Configuration to the windows machines.

The most important thing is that all of the windows machines come with built-in IPv6 Support but commonly most of the times users do not utilize IPv6, they use IPv4 in the network.

we will abuse this by default enabled function and say in the network “Hey, I'm an IPv6 DHCP Server let me give you the IPv6 configuration”, and once IPv6 is available in the network to machines the machines will prefer IPv6 over IPv4.

through this attack we can add users to the domain as an admin privileges

# **Process of Attack**

## **Step 1:**

Start the tool **mitm6** tool to assign the IPv6 Address to our targeted machine

```
mitm6 -i eth0 -d pkdc.local -hw raheem --ignore-nofqdn
```

```
mitm6 -i eth0 -d dtl.com --ignore-nofqdn
```

-i ⇒ Network Interface (eth0)

-d ⇒ The windows domain name (pkdc.local)

-hw ⇒ machine name/host name (raheem), name of windows machine

--ignore-nofqdn ⇒ it basically filters all the noisy stuff, only displays the progress information.
![[Pasted image 20251219195340.png]]


![[Pasted image 20251219195345.png]]

## **Step 2:**

Now start the tool which will help relay **ntlmrelayx** from impacket

```
./ntlmrelayx.py -6 -t ldaps://192.168.0.47 -wh fakewpad.pkdc.local -l lootdir
```

-6 ⇒ we are using IPv6 in this attack

-t ⇒ Our target in this instance (ldaps://192.168.0.47) - which is **DOMAIN CONTROLLER**

-wh ⇒ fake wpad Host name (its default from mitm6)

-l ⇒ all the data that ntlmrelayx gather will be stored in a new directory

-smb2support ⇒ Enable SMB 2 Support

![[Pasted image 20251219195637.png]]

## **Step 3:**

Now when the windows machine restarts the mitm6 assigns an IPv6 Configuration and the windows machine gets the IPv6 Address in the DNS configuration.

![[Pasted image 20251219195645.png]]

## **Step 4:**

Now on to the victim machine when the user log's in.

![[Pasted image 20251219195652.png]]

## **Step 5:**

The NTLM Credentials are sent to the mimt6 and it relays to the ntlmrelayx.

![[Pasted image 20251219195704.png]]

## **Step 6:**

Now here we can see there is a loot folder created, basically it contains all the User accounts , groups, computers all that knowledge about your Active Directory.

![[Pasted image 20251219195709.png]]

in the User Account's Description we can find passwords , most user's do that dumb act.

## **Step 7:**

Here we logged in to the Administrator account, so when the mitm6 gets he Admin credentials it sends to the mtlmrelayx and this will relay the credentials and creates User Account in the Domain.

![[Pasted image 20251219195715.png]]

now we relayed the user account's credentials and get the very valuable information about our active Directory Domain.

# **Mitigation**

MITM6 attacks can be difficult to detect and prevent, as they often involve sophisticated techniques and tools. However, there are steps that organizations and individuals can take to protect against these types of attacks:

- Disabling IPv6 if it is not used on your internal network will prevent Windows clients from querying for a DHCPv6 server thereby making it impossible to take over the DNS server.
- Disable the Proxy Auto detection via Group Policy. If your company uses a proxy configuration file internally (PAC file) it is recommended to explicitly configure the PAC URL instead of relying on WPAD to detect it automatically.
- In order to prevent NTLM relaying you should consider disabling it entirely and switch to Kerberos or, if that isnâ€™t possible, you should:
- enable SMB signing to prevent relaying to SMB by requiring all traffic to be signed
- enable LDAP signing to prevent unsigned connections to LDAP
- Enable extended protection for authentication which will prevent some relaying attacks by ensuring that the TLS channel used for the connection to the server is the same that the client uses when authenticating.