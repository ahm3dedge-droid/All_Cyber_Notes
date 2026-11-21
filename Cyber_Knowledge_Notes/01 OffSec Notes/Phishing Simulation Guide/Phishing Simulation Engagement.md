## **Phishing Engagement Workflow (Simplified & Professional)**

### **1. Domain Preparation**

- A **similar-looking domain** is purchased to mimic the real organization domain.
- This is usually bought from providers like Namecheap.
- The purpose is to **avoid easy detection** and make emails look legitimate.

---

### **2. Email Infrastructure Setup**

- An **SMTP relay service** is configured to send phishing emails.
- Common services include platforms like Mailgun.
- Sender email addresses are created to look real, such as:
    - `hr@example.com`
    - `itsupport@example.com`

---

### **3. Hosting Environment**

- Infrastructure (servers) is deployed on cloud platforms such as:
    - DigitalOcean
    - Amazon Web Services
    - Microsoft Azure

---

### **4. Phishing Framework Setup**

- A phishing tool like Gophish is used.
- Configuration includes:
    - Sender setup (SMTP integration)
    - Creation of **custom email templates**
    - Designing **trusted and realistic phishing pages**

---

### **5. Email Delivery & Targeting**

- Phishing emails are sent via platforms like Microsoft 365.
- Campaigns are **targeted** (specific users or departments).
- If the client has **SMTP IP whitelisting**, emails are more likely to bypass security filters.

---

### **6. Campaign Execution**

- The phishing campaign is launched.
- Metrics are monitored:
    - Email opens
    - Click rates
    - Credential submissions

---

### **7. Post-Exploitation Activities**

- If users fall for phishing:
    - Perform **post-exploitation analysis**
    - Check whether **Multi-Factor Authentication (MFA)** is enabled or not
- If MFA is **not enabled**, deeper access may be possible (only if allowed in scope).

---

### **8. Scope Validation**

- Before proceeding further:
    - Confirm whether **post-exploitation actions are in scope**
- If allowed → proceed with controlled testing
- If not → stop at phishing results and report findings

---

## **Simple Flow (Quick Understanding)**

1. Buy similar domain
2. Setup email sending (SMTP)
3. Deploy phishing tool
4. Create fake emails/pages
5. Send targeted emails
6. Track results
7. Test access (if allowed)