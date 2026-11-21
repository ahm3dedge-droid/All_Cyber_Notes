### 1. LANMAN (LM) Hash

- **Definition:** A legacy, highly insecure password hashing function used by early Microsoft operating systems (pre-Windows Vista) to store credentials.
    
- **Usage:** Obsolete and disabled by default in modern Windows environments, though it is occasionally found in misconfigured or extremely outdated legacy systems.
    
- **Bit Size:** 128 bits (16 bytes) total, constructed from two 64-bit halves.
    
- **Hash Function:** Based on the DES block cipher.
    
    - **Algorithm:** The password is converted to uppercase, padded with null bytes to exactly 14 characters, and split into two 7-byte halves. Each 7-byte half is used as a DES key to encrypt a constant ASCII string `KGS!@#$%`. The two resulting 8-byte ciphertexts are concatenated.
        
    - **Formula:** \text{LM Hash} = \text{DES}_{\text{key1}}(\text{"KGS!@#\$%"}) \parallel \text{DES}_{\text{key2}}(\text{"KGS!@#\$%"})
        
- **Mandatory Cyber Details:**
    
    - **No Salting:** Completely unsalted, making it highly vulnerable to Rainbow Table attacks.
        
    - **Entropy Loss:** Forcing all characters to uppercase destroys case-sensitive entropy.
        
    - **Password Splitting:** Because the 14-character password is split in half, attackers only need to brute-force a maximum 7-character password twice. This exponentially reduces the cracking time compared to a full 14-character string.
        
    - **Visual Telltale:** If a user's password is 7 characters or less, the second half of the hash will always equate to the static, recognizable hex value `0xAAD3B435B51404EE`.
        

---

### 2. NTLM (NT) Hash

- **Definition:** The direct successor to the LM hash, providing a stronger, case-sensitive method for storing Windows passwords locally and in Active Directory.
    
- **Usage:** Still heavily used today for local SAM database storage, NTDS.DIT (Active Directory), and fallback network authentication (NTLMv1).
    
- **Bit Size:** 128 bits (16 bytes).
    
- **Hash Function:** Uses the MD4 cryptographic hashing algorithm.
    
    - **Algorithm:** It takes the plaintext password, converts it to Unicode (UTF-16 Little-Endian), and hashes it directly with MD4.
        
    - **Formula:** NT Hash=MD4(UTF-16-LE(Password))
        
- **Mandatory Cyber Details:**
    
    - **No Salting:** Like LM, NT hashes are unsalted. Pre-computed Rainbow Tables and dictionary attacks remain highly effective for offline cracking.
        
    - **Pass-the-Hash (PtH):** A critical vulnerability. Attackers do not need to crack the NT hash to authenticate; they can extract it from memory (e.g., using Mimikatz) and inject it directly into authentication protocols to impersonate users laterally across a network.
    - **Structural Improvement:** Unlike LM, NT hashes preserve case sensitivity and do not split the password into halves, significantly increasing the required keyspace for brute-force attacks.
        

---

### 3. NTLMv2 Hash (and NetNTLMv2)

- **Definition:** A network authentication protocol and cryptographic hash designed to mitigate the vulnerabilities of NTLMv1 by introducing challenge-response nonces and variable salting.
    
- **Usage:** The standard fallback authentication protocol for Windows domains when Kerberos fails or is unavailable. Unlike NT hashes, NTLMv2 hashes are dynamically generated for network handshakes and are generally not stored "at rest".
    
- **Bit Size:** The base NTLMv2 hash itself is 128 bits (16 bytes). However, the full network response (NetNTLMv2) is variable in length due to the dynamic client blob attached to it.
    
- **Hash Function:** Uses HMAC-MD5.
    
    - **Algorithm:** It uses the underlying NT Hash as a cryptographic key to HMAC-MD5 the concatenated uppercase username and domain name. For the actual network authentication (NetNTLMv2), this resulting hash is mixed via HMAC-MD5 with a Server Challenge and a dynamically generated Client Nonce/Blob.
        
    - **Formula:** NTLMv2 Hash=HMAC-MD5(NT Hash,UPPER(Username)∥Domain)
        
- **Mandatory Cyber Details:**
    
    - **Salted (Effectively):** The incorporation of the username and domain acts as a cryptographic salt, rendering standard Rainbow Tables useless.
        
    - **Replay Protection:** The Server Challenge and Client Nonce mathematically tie the authentication to a specific session, preventing simple packet-replay attacks.
        
    - **Relay Attacks:** While traditional Pass-the-Hash is not directly possible with NetNTLMv2 responses, intercepted handshakes are highly susceptible to **NTLM Relay Attacks** (e.g., via tools like Responder or ntlmrelayx). Attackers can forward the authentication attempt to another machine unless protections like SMB Signing or LDAP Channel Binding/EPA are strictly enforced.
        
    - **Offline Cracking:** If an attacker intercepts the NetNTLMv2 challenge-response handshake, they can crack it offline (using Hashcat or John the Ripper) via dictionary attacks to recover the original plaintext password.



