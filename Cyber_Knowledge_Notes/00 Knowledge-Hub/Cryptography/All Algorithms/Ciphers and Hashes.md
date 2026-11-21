### 1. The Symmetric Ciphers (The Lockboxes)

_Same key used to lock (encrypt) and unlock (decrypt)._

- **RC4 (Rivest Cipher 4):** A _stream cipher_ (encrypts data bit-by-bit continuously). It was incredibly fast and widely used in early web traffic (SSL) and Wi-Fi (WEP). **Status:** Broken and obsolete.
    
    - _Mental Sticky Note:_ The fast runner who tripped and fell.
        
- **DES (Data Encryption Standard):** A _block cipher_ (encrypts data in 64-bit chunks). It uses a tiny 56-bit key. **Status:** Obsolete. Modern computers can brute-force a 56-bit key in hours.
    
    - _Mental Sticky Note:_ The retired grandfather of encryption.
        
- **3DES (Triple DES):** Literally just running DES three times in a row on the same data to artificially make the key longer (up to 168 bits) because people were panicking about DES being cracked. **Status:** Slow, clunky, and being phased out.
    
    - _Mental Sticky Note:_ Three grandfathers in a trench coat.
        
- **AES (Advanced Encryption Standard):** The modern gold standard block cipher. It processes data in 128-bit blocks. The numbers **128, 192, and 256** refer to the size of the _key_. AES-256 is considered military-grade and quantum-resistant. **Status:** The undisputed champion.
    
    - _Mental Sticky Note:_ The modern bank vault.
        

---

### 2. The Asymmetric Ciphers (The Mailboxes)

_Two keys: A Public Key to lock (anyone can drop a letter in), and a Private Key to unlock (only you can open the box)._

- **RSA (Rivest-Shamir-Adleman):** The mathematical foundation of the internet. It relies on the extreme difficulty of factoring massive prime numbers. It is incredibly secure but very _slow_. Therefore, it is almost never used to encrypt huge files; instead, it is used to securely swap AES keys across the internet, or for Digital Signatures.
    
    - _Mental Sticky Note:_ The slow, heavy, impenetrable mathematical fortress.
        

---

### 3. Hashes & MACs (The Fingerprints)

_One-way math. You can turn a file into a hash, but you cannot turn a hash back into a file. Used to prove something hasn't been altered._

- **MD5 (Message-Digest 5):** Creates a 128-bit hash. **Status:** Cryptographically broken. It is vulnerable to "collisions" (attackers can make a malicious file generate the exact same hash as a safe file). Only use it to check if a file downloaded correctly, _never_ for passwords or security.
    
    - _Mental Sticky Note:_ The smudged fingerprint scanner.
        
- **SHA (Secure Hash Algorithm):** A family of hashes created by the NSA.
    
    - **SHA-1 (160-bit):** Broken, do not use.
        
    - **SHA-2 (SHA-256, SHA-512):** The current industry standard. Extremely secure. Used everywhere from SSL certificates to Bitcoin.
        
    - _Mental Sticky Note:_ The flawless, modern biometric scanner.
        
- **HMAC (Hash-based Message Authentication Code):** Combines a hash algorithm (like SHA-256) with a _secret password_. A normal hash only proves the data didn't change (Integrity). An HMAC proves the data didn't change _and_ it came from someone who holds the secret key (Authenticity).
    
    - _Mental Sticky Note:_ A wax seal stamped with a secret family ring.
        

---

### 4. Wireless Protocols (The Wi-Fi Bouncers)

_The evolution of trying to secure radio waves floating in the air._

- **WEP (Wired Equivalent Privacy):** The original Wi-Fi security. It used the **RC4** algorithm but implemented it terribly. Attackers can capture a few minutes of Wi-Fi traffic and crack the password instantly. **Status:** Utterly useless.
    
    - _Mental Sticky Note:_ A screen door on a submarine.
        
- **TKIP (Temporal Key Integrity Protocol):** A band-aid protocol. When WEP was cracked, hardware couldn't support heavy new encryption. TKIP kept RC4 but rapidly _changed the keys per packet_ so attackers couldn't gather enough data to break it. **Status:** Deprecated.
    
    - _Mental Sticky Note:_ A shell game trying to hide RC4's flaws.
        
- **WPA (Wi-Fi Protected Access):** The temporary protocol that wrapped WEP in TKIP to stop the bleeding while the industry built WPA2 (which finally ditched RC4 and moved to AES).
    
    - _Mental Sticky Note:_ The duct-tape fix holding routers together in the mid-2000s.