# **SMB Relay Attack**

SMB Relay, Basically in this attack we use the same Technique as like we did used in LLMNR Poisoning, we start the **responder** which is used to respond to the Broadcast requests and also run the **ntlmrelayx** (on our kali machine) which is used to relay those Captured Credentials/Hashes, in this attack instead of cracking those hashed we relay those and use them to get more Information. now on the target windows machines that has SMB signing disabled we (as a victim) try to access the **\\network_resource**, this will cause an event.

and the windows machine let's say its host name is “RAHEEM”, this will go to the DNS and searches for this network resource when the DNS fails to find this network resource then this will message broadcast this message and sends to all hosts in the network and our attacker machine which is our kali machine, it says “Hey i know where this network resource, give me your password hash and i will you connect to that network resource” the windows host will provide that hash.  Responder will capture this hash, pass it to ntlmrelayx, which will relay the credentials to the targets in our targets file.

# **Relay Attack:**
- **Interception:**
  An attacker intercepts the initial authentication attempt.
- **Relay:**
  Instead of trying to crack the challenge-response (which is difficult), the attacker relays the authentication attempt to another SMB server.
- **Impersonation:**
  The second server sees the relayed request as legitimate and grants access, believing the attacker is the authenticated user.

# **Detect if the Target is Vulnerable?**

Run this Nmap Script on Target

**COMMAND:** 
```
nmap --script=smb2-security-mode.nse -p445 10.0.0.0/24
```

# **Let's to Perform Attack**

## 1. Edit Responder Config file
![[Pasted image 20251219194648.png]]

## 2. Run the Responder
![[Pasted image 20251219194704.png]]

## 3. Run the **NTLMRelayX** Tools for relay

```
sudo ntlmrelayx.py –tf targets.txt –smb2support
```

![[Pasted image 20251219194712.png]]

## 4. An Event Occur on Windows Machine.
![[Pasted image 20251219194738.png]]

## 4. The SAM File with Hashes Dumped Here at the **NTLMRelayX** Tool.

![[Pasted image 20251219194749.png]]

we can do so many things with SMB relay attacks.

---
---
# **Mitigation Strategies of SMB Relay Attacks**

![[Pasted image 20251219194754.png]]

To enforce SMB signing, enable the following policies in Computer Configuration > Policies > Windows Settings > Security Settings > Local Policies > Security Options:

**On the client side:**

- Microsoft network client: Digitally sign communications (always)
- Microsoft network client: Digitally sign communications (if server agrees)

**On the server side:**

- Microsoft network server: Digitally sign communications (always)
- Microsoft network server: Digitally sign communications (if client agrees)

![[Pasted image 20251219194800.png]]