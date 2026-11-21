# **NTLM**

New Technology LAN Manager (NTLM) is an Authentication Protocol, which is widely used in windows domains to authenticate Users. it basically works on a challenge-response mechanism to authenticate users. NTLM is deprecated Authentication Protocol, now from 2000 the Kerberos authentication protocol is the default Authentication Protocol Used by the Windows Domains. when ever the Kerberos fails then NTLM will takes it's place.

## **How NTLM Authentication Works?**

![[Pasted image 20251219191427.png]]
1. user asks for the access to any network resource.
2. server sends the challenge message to the client.
3. client sends the solved challenge message to the server.
4. server sends the challenge and the response to the Domain Controller.
5. Domain Controller compares the challenge and response that the client gave to it, and authenticate user to the service.
6. The server sends the response to the Client.

# **Detailed Explanation**

1. A user accesses a client computer and provides a domain name, user name, and a password. The client computes a cryptographic hash of the password and discards the actual password. The client sends the user name to the server (in plaintext).
2. The server generates a 16-byte random number, called a challenge, and sends it back to the client.
3. The client encrypts this challenge with the hash of the user's password and returns the result to the server. This is called the response.
4. The server sends the following three items to the domain controller:
5. User Name
6. Challenge sent to the client
7. Response received from the client
8. The domain controller uses the user name to retrieve the hash of the user's password. It compares the encrypted challenge with the response by the client (in step 4). If they are identical, authentication is successful, and the domain controller notifies the server.
9. The server then sends the appropriated response back to the client.