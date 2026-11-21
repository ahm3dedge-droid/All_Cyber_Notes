# 📧 SPF • DKIM • DMARC — 60-Second Master Cheat Sheet

---

## One-Line Purpose (Golden Rule)

|Control|One-Line Meaning|
|---|---|
|**SPF**|Who is allowed to send email for this domain?|
|**DKIM**|Was the email changed on the way?|
|**DMARC**|What should we do if checks fail?|

---

## Full Flow (Super Short)

1️⃣ Email is sent  
2️⃣ Receiver checks **SPF** (sender IP)  
3️⃣ Receiver checks **DKIM** (signature)  
4️⃣ **DMARC** evaluates results + alignment  
5️⃣ Final action: **Inbox / Spam / Reject**

---

## What Each One Checks

|Control|Checks|Does NOT Check|
|---|---|---|
|SPF|Sending server IP|Email content|
|DKIM|Message integrity|Server IP|
|DMARC|SPF/DKIM + alignment|Malware|

---

## PASS / FAIL Logic (Very Important)

### SPF
- IP allowed → **PASS**
- IP not allowed → **FAIL**

### DKIM
- Signature valid → **PASS**
- Email altered / bad key → **FAIL**

### DMARC (Core Rule)
```
(SPF PASS + aligned)
        OR
(DKIM PASS + aligned)
            ↓
        DMARC PASS
```

❌ If both fail or not aligned → DMARC FAIL

---

## Alignment (This Is Where Beginners Get Confused)
**Alignment = Same domain as “From:”**

|Item|Example|
|---|---|
|Visible From|[user@company.com](mailto:user@company.com)|
|SPF aligned|MAIL FROM = company.com|
|DKIM aligned|d=company.com|

➡️ At least **one must align**

---

## DNS Record Examples (Minimal & Real)
### SPF
```
v=spf1 include:_spf.google.com -all
```

### DKIM
```
google._domainkey.company.com
TXT "v=DKIM1; p=PUBLICKEY"
```

### DMARC
```
v=DMARC1; p=quarantine; rua=mailto:dmarc@company.com
```

---
## Final Outcomes (Decision Table)

|SPF|DKIM|DMARC Policy|Result|
|---|---|---|---|
|PASS|PASS|any|Inbox|
|FAIL|PASS|any|Inbox|
|FAIL|FAIL|none|Deliver (monitor)|
|FAIL|FAIL|quarantine|Spam|
|FAIL|FAIL|reject|Blocked|

---
## Common Real-World Truths 🧠

- SPF **breaks on forwarding**
- DKIM **survives forwarding**
- DMARC **enforces trust**
- DMARC = **visibility + control**
- One domain = **one SPF record only**

---
## One-Line Memory Story (Never Forget)
> **SPF asks:** “Who sent it?”  
> **DKIM asks:** “Was it changed?”  
> **DMARC decides:** “What do we do?”

---
