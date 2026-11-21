# Mimikatz Attacks – Domain-Categorized Mindmap (CRTP)

**Goal:** Reduce cognitive load by grouping Mimikatz usage by _domain context_ rather than by individual commands. This aligns well with CRTP labs and real-world AD attack paths.

---

## 1. Local Machine / Host Context

_(You have local access; domain interaction may or may not exist yet)_

### 1.1 Credential Material in Memory

- Plaintext credentials (where possible)
    
- NTLM hashes
    
- Kerberos tickets cached in LSASS
    

### 1.2 Logon Sessions

- Interactive logons
    
- Service logons
    
- Scheduled task logons
    
- RDP sessions
    

### 1.3 Token & Privilege Abuse (Local)

- Token enumeration
    
- Token impersonation
    
- Privilege escalation prerequisites (SeDebugPrivilege)
    

**Mental model:**

> “What secrets does _this machine_ currently hold because of who logged into it?”

---

## 2. Local Administrator → Domain-Relevant Impact

_(Still local execution, but domain credentials are exposed)_

### 2.1 Cached Domain Credentials

- Domain user NTLM hashes
    
- Domain admin hashes (if logged in)
    

### 2.2 Kerberos Artifacts (Local Cache)

- TGTs (krbtgt-signed)
    
- TGS tickets for domain services
    

### 2.3 Credential Reuse Potential

- Pass-the-Hash (PTH)
    
- Pass-the-Ticket (PTT)
    

**Mental model:**

> “Which _domain identities_ touched this box and left credentials behind?”

---

## 3. Active Directory User Context

_(You are a domain user; no admin rights yet)_

### 3.1 Kerberos Abuse (User-Level)

- Ticket extraction for current user
    
- Service ticket reuse
    

### 3.2 Delegation Exposure (If Applicable)

- Unconstrained delegation remnants
    
- Service accounts with delegation
    

### 3.3 Lateral Movement Enablement

- Using extracted tickets to access domain services
    

**Mental model:**

> “How far can a _normal domain user_ go using only Kerberos material?”

---

## 4. Domain Administrator Context

_(High-impact, high-risk, exam-critical)_

### 4.1 NTDS.dit–Related Attacks

- DCSync (logical replication abuse)
    
- Dumping domain password data
    

### 4.2 KRBTGT Abuse

- Golden Ticket creation
    
- Long-term domain persistence
    

### 4.3 Trust Exploitation

- Child → Parent domain abuse
    
- Inter-domain ticket forging
    

**Mental model:**

> “I am the domain. What secrets can I mint or replicate?”

---

## 5. Domain Controller Context

_(Execution on DC or equivalent replication privileges)_

### 5.1 LSASS on DC

- Domain-wide credential exposure
    
- Service account secrets
    

### 5.2 Replication Attacks

- Full directory credential sync
    

### 5.3 Persistence Mechanisms

- Golden Tickets
    
- Skeleton Key–style memory abuse
    

**Mental model:**

> “This is the identity source of truth—compromise here is total.”

---

## 6. Cross-Domain / Forest-Level Attacks

_(Advanced CRTP scenarios)_

### 6.1 Trust Keys & Tickets

- Inter-realm trust keys
    
- Forged tickets across domains
    

### 6.2 Forest Persistence

- Enterprise-level Golden Tickets
    
- Cross-forest lateral movement
    

**Mental model:**

> “How identities flow _between_ domains—and how to hijack that flow.”

---

## 7. Persistence-Focused Usage (Post-Exploitation)

_(Regardless of domain level)_

- Golden Tickets (long-lived access)
    
- Cached credential planting
    
- Memory-resident access paths
    

**Mental model:**

> “How do I stay without touching disk or accounts?”

---

## 8. Defensive Awareness (CRTP Mindset Bonus)

_(Helps with blue-team questions and stealth)_

- LSASS protections (PPL)
    
- Credential Guard impact
    
- Event traces of replication abuse
    

---

## One-Line Exam Orientation Map

- **Local box** → credentials in memory
    
- **Domain user** → Kerberos leverage
    
- **Local admin** → domain creds exposure
    
- **Domain admin** → DCSync & Golden Tickets
    
- **DC** → full identity compromise
    
- **Forest** → trust abuse
    

---

If you want, I can:

- Convert this into a **visual diagram (ASCII / draw.io structure)**
    
- Map **specific CRTP labs → each branch**
    
- Add a **"When to use this" decision tree**


| Context                   | Primary Action                      |
| ------------------------- | ----------------------------------- |
| Local box                 | sekurlsa::logonpasswords            |
| Domain user               | kerberos::list /export              |
| Local admin               | sekurlsa::pth                       |
| Domain admin              | lsadump::dcsync                     |
| DC                        | sekurlsa::logonpasswords (on DC)    |
| Forest                    | kerberos::golden (Enterprise Admin) |