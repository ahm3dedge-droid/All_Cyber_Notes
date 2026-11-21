![[Pasted image 20251219200837.png]]

**DCsync** is an attack technique in Active Directory where an attacker tricks a Domain Controller (DC) into thinking they are another Domain Controller. This allows the attacker to request and receive password hashes for any account in the domain, including those of high-privilege accounts like `krbtgt` and `Administrator`.

### **How It Works:**

- **Normal Operation:** Domain Controllers synchronize user information, including password hashes, with each other to keep the directory up-to-date.
- **DCsync Attack:** The attacker uses tools like Mimikatz to pretend to be a Domain Controller and asks another DC for the password data. If successful, the attacker can then use these hashes to access accounts or perform further attacks.

### **Key Points:**

- **No Direct Access Needed:** The attacker doesn’t need to log into the DC itself; they just need the right permissions.
- **High Privileges Required:** The attacker typically needs Domain Admin or similar high-level privileges to perform a DCsync attack.

### **Why It’s Dangerous:**

Once the attacker has password hashes, they can impersonate users, escalate privileges, or create Golden Tickets, leading to complete control over the domain.

## **Attack Process:**

1. Compromise a standard or non-privileged user account with “Replicate Directory Changes” permission.
2. Discover a DC in the specified domain name.
3. Request the DC to replicate sensitive information such as password hashes using the Microsoft Directory Replication Service Remote (MS-DRSR) protocol.
4. Obtain NTLM hashes of potentially useful accounts such as KRBTGT and Administrators.
5. Create a Golden Ticket and run Pass the Ticket (PTT) attacks to move laterally.