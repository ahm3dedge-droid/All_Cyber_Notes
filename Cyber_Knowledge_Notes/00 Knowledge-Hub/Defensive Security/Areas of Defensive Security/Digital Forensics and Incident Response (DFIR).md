## Digital Forensics and Incident Response (DFIR)
This section is about Digital Forensics and Incident Response (DFIR), and we will cover:

**1.1 Digital Forensics**
**1.2 Incident Response**
**1.3 Malware Analysis**

---
### 1.1 Digital Forensics
Digital forensics applies scientific methods to **collect, preserve, analyze, and present digital evidence**.
##### Key Forensic Areas
- **File System Analysis**
    - Installed software
    - Created, modified, deleted files
    - Partially overwritten data
        
- **Memory (RAM) Analysis**
    - Detect fileless malware
    - Capture running processes and artifacts
        
- **System Logs**
    - User actions, authentication, system events
    - Even deleted logs may leave traces
        
- **Network Logs**
    - Traffic patterns
    - Evidence of attacks or data exfiltration
##### Purpose in Defensive Security
- Identify attackers
- Reconstruct attack timeline
- Support incident response and legal actions

---
### 1.2 Incident Response (IR)
Incident response defines the **structured approach** to handle cybersecurity incidents and reduce impact.

##### What Is an Incident?
- Cyber attacks (ransomware, data breaches, DDoS)
- Intrusion attempts
- Misconfigurations
- Policy violations

##### Incident Response Phases

1. **Preparation**
    - Trained team
    - Tools, procedures, and preventive controls
        
2. **Detection and Analysis**
    - Identify incidents
    - Assess scope and severity
		
3. **Containment, Eradication, and Recovery**
    - Stop spread of attack
    - Remove threat
    - Restore systems securely
        
4. **Post-Incident Activity**
    - Reporting
    - Lessons learned
    - Improve defenses

![[Pasted image 20260121084306.png]]

---
### 1.3 Malware Analysis
**Malware** refers to malicious software designed to damage, disrupt, or gain unauthorized access.

#### Common Malware Types
- **Virus**
    - Attaches to programs
    - Spreads between systems
    - Damages or alters files
        
- **Trojan Horse**
    - Appears legitimate
    - Executes hidden malicious actions
        
- **Ransomware**
    - Encrypts user data
    - Demands payment for decryption key


#### Malware Analysis Techniques
##### Static Analysis
- Analyze malware **without executing it**
- Inspect code, strings, and structure
- Requires knowledge of assembly and binaries

##### Dynamic Analysis
- Execute malware in a **controlled environment**
- Observe runtime behavior:
    - Network connections
    - File changes
    - Process creation