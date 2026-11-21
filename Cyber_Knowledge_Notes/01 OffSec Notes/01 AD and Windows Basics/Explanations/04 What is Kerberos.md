# **Kerberoas**

### _Kerberos is an authentication protocol. It's the default authentication protocol on Windows versions above W2k, replacing the NTLM authentication protocol._

Kerberos is an authentication protocol that operates based on tickets, allowing nodes to securely prove their identity to one another over a non-secure network. It primarily aims at a client-server model and provides mutual authentication, where the user and the server verify each other's identity. The Kerberos protocol messages are protected against eavesdropping and replay attacks, and it builds on symmetric-key cryptography, requiring a trusted third party.

Kerberoas is the Authentication Protocol used in Microsoft Active Directory Environment to Authenticate Users to the Services or Network Resources. It works on the Tickets like TGT and TGS.

____________________________________________________________________

# **How Kerberos Works?**

![[Pasted image 20251219191955.png]]

1. A user login to the client machine. The client does a plaintext request (TGT). The message contains: (ID of the user; ID of the requested service (TGT); The Client Net address (IP); validation lifetime)
2. The Authentication Server will check if the user exists in the KDC database.

If the user is found, it will randomly generate a key (session key) for use between the user and the Ticket Granting Server (TGS).

The Authentication Server will then send two messages back to the client:

- One is encrypted with the TGS secret key.
- One is encrypted with the Client secret key.

NOTE:

The TGS Session Key is the shared key between the client and the TGS.

The Client secret key is the hash of the user credentials (username+password).

1. The client decrypts the key and can logon, caching it locally. It also stores the encrypted TGT in his cache.

When accessing a network resource, the client sends a request to the TGS with the resource name he wants to access, the user ID/timestamp and the cached TGT.

1. The TGS decrypts the user information and provides a service ticket and a service session key for accessing the service and sends it back to the Client once encrypted.
2. The client sends the request to the server (encrypted with the service ticket and the session-key)
3. The server decrypts the request and if its genuine, it provides service access.

____________________________________________________________________

# **Components**

**Domain Controller (DC)**

Domain Controller is the main part, here it is acting as a Key Distribution Center.

**User's Workstation**

This is the user who wants to access the service in the network.

**Application Server**

This is the Server where the service is running. like in this case there is an Application is running.

**Key Distribution Center (KDC)**

This is actually our Domain Controller (DC) which is playing a Key Distribution Center (KDC) role here. KDC job is to provide Ticket Granting Tickets and Ticket Granting Service (TGS) Tickets.

**Ticket Granting Ticket (TGT)**

This is the first ticket that is used for initial Authentication, this ticket is issued by the KDC in 1st step.

**Ticket Granting Service (TGS) Ticket**

TGS is the second ticket that is also issued by the KDC and this TGS ticket is then used to access the network resource.

## Is Kerberos secure?

The Kerberos protocol is considered secure. It has been widely implemented for decades, and it is considered a mature and safe mechanism for authenticating users. Kerberos uses strong cryptography, including secret-key encryption, to protect sensitive data.

Security researchers have been investigating Kerberos since it was first published. Weaknesses have been found in specific Kerberos implementations, as well as in the protocol itself. Those weaknesses have been addressed, and Kerberos remains fundamental for authentication in the internet.

Some of the historic weaknesses in Kerberos as used in Windows networks were [summarized in a 2015 blog post](https://dfirblog.wordpress.com/2015/12/13/protecting-windows-networks-kerberos-attacks/) by security researcher Elmar Nabigaev. They included the following:

- **Pass-the-key attack.** This is a form of [pass-the-hash attack](https://www.techtarget.com/searchsecurity/definition/pass-the-hash-attack) in which attackers impersonate authorized users by replaying their credentials.
- **Pass-the-ticket attack.** Attackers intercept and reuse tickets sent to or from an authenticated user to impersonate them and reuse their service tickets.
- **Golden ticket attack.** This is an attack that uses access to the Windows [domain controller](https://www.techtarget.com/searchwindowsserver/definition/domain-controller) to create credentials that give unlimited access to application services.

To keep Kerberos secure, you should stay up to date with Kerberos security vulnerabilities and stay current with software updates that mitigate or remediate flaws, such as the "Kerberoasting" attack used in the [SolarWinds supply chain attacks](https://www.techtarget.com/searchsecurity/news/252493761/SolarWinds-breach-highlights-dangers-of-supply-chain-attacks) in 2020.

###########################################################################################

# **6 STEP PROCESS**

![[Pasted image 20251219192117.png]]

**DETAILED OVERVIEW**

![[Pasted image 20251219192122.png]]

**Step 1: (AS-REQ)**

The user sends the requests TGT to the KDC with some data that is timestamp basically and this is encrypted with user password's NTLM hash, the user doesn't sends the actual password, hence the KDC knows everyone's password hash so the KDC will decrypt this data which is basically a timestamp encrypted with users password hash. this verifies that the request is coming from legitimate user.

**Step 2: (AS-REP)**

_note: there is a built-in account in the widows domain controller which is_ _**KRBTGT**_ _and only, The system knows the password of this account, this account is disabled and cannot be logged in and cannot be enabled._

Now the KDC will send back 2 things to the user, “**The session key**” and "**The TGT ticket**”, the session key is encrypted with the users password NTLM hash and the TGT ticket is encrypted with KRBTGT's account's password hash. The TGT ticket data also contains the session key.

**NOTE: Step 1 and Step 2 is handled by the [Authentication Service]**

**Step 3: (TGS-REQ)**

Now the user send the request to the KDC which has 2 things (the “**TGT Ticket**” and the "**Some data (****username, timestamp****)**" which is encrypted with session key).

In this request the user is requesting a Service Ticket to access the SQL service.

how the user is able to encrypt the data with session key? as we know, in the previous step KDC sends the session key which is encrypted with user's password NTLM hash, and the user knows his password hash resulting in decrypting the session key, that's how the user gets the session key.

now KDC receives the TGT Ticket, KDC knows the password hash of KRBTGT's account so it uses it to decrypt the TGT ticket as it is encrypted with KRBTGT's account's password hash, and obtain the session key which is in the TGT Ticket. now with that session key KDC will Decrypt the Data (username, timestamp) that is sent along with the TGT Ticket verifying the user's legitimacy.

**Step 4: (TGS-REP)**

The KDC will now send 2 things to the user, The "**Service Ticket**" and the "**New Session key**". the Service Ticket contains the New Session key and it is encrypted with the Service account password NTLM hash in this case it is SQL Service, and the New Session Key is encrypted with the User's Password so the user can decrypt and can obtain the new session key for the next step.

**NOTE: Step 3 and Step 4 is handled by the [Ticket Granting Service]**

**Step 5:** **(AP-REQ)**

Now the user is sending 2 things to the Service account. The "**Service Ticket**" and ("**Some Data** which is encrypted with the new session key").

The Service Ticket also contains the new session key in it.

The Service ticket is encrypted with the service account password hash, in this case it's encrypted with the SQL Service Account Password hash, the Service knows it's own password hash so it can decrypt the Service ticket and get the new session key.

Now with the obtained new session key, The SQL Server will decrypt the data in TGS Ticket which is encrypted with this new session key before.

**Step 6: (AP-REP)**

Now the SQL server will decrypt the Service Ticket which is encrypted with the service account's password hash and obtains the new session key, and with that new session key it try to decrypt the data, Here if the data decrypts successfully, then it proves that the both session keys are same. The user is now legitimate because the session keys is only be same when the user has it's own password hash and only then it can has the new session key which is previously encrypted with the user's password hash sent by the TGS and it all proves that the user is the user who it claims to be.

Now, after all this verification process the service account will grant user access to the service.

###########################################################################################

Best Explanation Video of Kerberos

[https://www.youtube.com/watch?v=snGeZlDQL2Q&list=PL3B8L-z5QU-Z0bWmjwgUSLGTzm1k_kVZo](https://www.youtube.com/watch?v=snGeZlDQL2Q&list=PL3B8L-z5QU-Z0bWmjwgUSLGTzm1k_kVZo)

Awesome YouTube Playlist Explaining Kerberos Attacks

[https://www.youtube.com/playlist?list=PL3B8L-z5QU-Z0bWmjwgUSLGTzm1k_kVZo](https://www.youtube.com/playlist?list=PL3B8L-z5QU-Z0bWmjwgUSLGTzm1k_kVZosdsd)