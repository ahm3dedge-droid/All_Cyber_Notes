## 1. LSASS Local Security Authority Sub-system Service) - Memory Dump
- **What it is**: LSASS is a process that handles authentication (logins, security tokens). It stores creds in memory for active sessions.
- **Creds you get**: Plaintext passwords (if cached), NTLM hashes, AES keys, Kerberos tickets (TGTs/TGS for network access).
- **Prerequisites**: Local admin/SYSTEM rights; tool like SafetyKatz/Mimikatz; often need to bypass AV/AMSI.
- **How it works**: Tool injects into LSASS or dumps its memory, decrypts using Windows APIs. E.g., command: SafetyKatz.exe "`sekurlsa::logonpasswords`" "exit". For offline: Create minidump (via Task Manager or procdump.exe), then parse: SafetyKatz.exe "`sekurlsa::minidump lsass.dmp`" "`sekurlsa::logonpasswords`".
- **Notes**: High detection risk (EDR watches LSASS). Use minidumps for evasion. On servers, dumps admin sessions for domain escalation.
---
## 2. SAM (Security Accounts Manager) Database
- **What it is**: A file-based database in %SystemRoot%\System32\config\SAM that stores local user accounts.
- **Creds you get**: NTLM hashes for local users (e.g., local Administrator).
- **Prerequisites**: Local admin; access to system files (e.g., boot to offline mode or use shadow copies).
- **How it works**: Copy SAM + SYSTEM hives (for decryption keys), then extract: SafetyKatz.exe "`lsadump::sam`". Offline: Use tools like secretsdump.py or reg save.
- **Notes**: Only local creds (not domain). Servers often have local admins synced to domain—useful for initial foothold.
---
## 3. LSA Secrets (Local Security Authority Secrets)
- **What it is**: Registry-stored secrets for services/autologon.
- **Creds you get**: Service account passwords, autologon creds, DPAPI keys.
- **Prerequisites**: Local admin; elevated process.
- **How it works**: Patch LSASS to reveal: SafetyKatz.exe "`lsadump::lsa /patch`". Dumps from registry (HKLM\SECURITY\Policy\Secrets).
- **Notes**: Great for services on servers (e.g., SQL service accounts). Enable LSA Protection to block.
---
## 4. Credential Manager (Windows Vault)
- **What it is**: Stores creds for apps/networks (e.g., saved WiFi, RDP).
- **Creds you get**: Encrypted passwords/tokens for web, networks, generics.
- **Prerequisites**: User-level access (for own vault); admin for others; DPAPI master key.
- **How it works**: Use vaultcmd /list to enum, then Mimikatz: `privilege::debug` + `dpapi::cred` `/in:<vault file>`. Files in %APPDATA%\Microsoft\Credentials.
- **Notes**: On servers, dumps service creds. Decrypt with user's DPAPI key.
---
## 5. DPAPI (Data Protection API) Master Keys
- **What it is**: System for encrypting user data (e.g., browser creds).
- **Creds you get**: Master keys to decrypt other stored creds.
- **Prerequisites**: User access (own keys); admin for system/master.
- **How it works**: Dump from LSASS or files: SafetyKatz.exe "`dpapi::masterkey`". Files in %APPDATA%\Microsoft\Protect.
- **Notes**: Chains to browser/RDP dumping. Servers hold service DPAPI keys.
---
## 6. Browser Credential Stores
- **What it is**: Browsers like Chrome/Edge store logins in encrypted databases.
- **Creds you get**: Website usernames/passwords.
- **Prerequisites**: User access to profile; DPAPI key for decryption.
- **How it works**: For Chrome: Copy Login Data file (*%LOCALAPPDATA%\Google\Chrome\User Data\Default*), decrypt with DPAPI: Tools like SharpChrome or Mimikatz module `dpapi::chrome`.
- **Notes**: On servers, admins browse as SYSTEM—dump for domain creds. Multi-browser (Edge similar).
---
## 7. RDP (Remote Desktop) Saved Credentials
- **What it is**: Saved RDP connections store creds in .rdp files or Credential Manager.
- **Creds you get**: RDP passwords for remote machines.
- **Prerequisites**: Access to user profile; DPAPI for decryption.
- **How it works**: Files in %APPDATA%\Microsoft\Remote Desktop; Dump via Credential Manager or cmdkey /list + Mimikatz to decrypt.
- **Notes**: Common on servers for admin remoting. Leads to lateral movement.
---
## 8. Scheduled Tasks with Embedded Credentials
- **What it is**: Tasks (via Task Scheduler) can store creds for running as users.
- **Creds you get**: Passwords for task accounts.
- **Prerequisites**: Admin to read task XML/files.
- **How it works**: Export tasks: schtasks /query /xml, parse for `<Credentials>` (encrypted); Decrypt with DPAPI or Mimikatz.
- **Notes**: Servers run many tasks—e.g., backups with service creds.

## 9. Registry Hives with Credentials
- **What it is**: Registry keys store creds (e.g., unattended installs, autologon).
- **Creds you get**: Plaintext/hashed creds for auto-setup.
- **Prerequisites**: Admin to read protected hives.
- **How it works**: Query: reg query HKLM\SOFTWARE\Microsoft\Windows\CurrentVersion\Unattended; Or dump hives offline.
- **Notes**: Rare but gold on fresh servers. Also, Winlogon for autologon: reg query HKLM\SOFTWARE\Microsoft\Windows NT\CurrentVersion\Winlogon.
---
## 10. Configuration Files with Hardcoded Credentials
- **What it is**: Apps/services store creds in files (e.g., web.config, scripts).
- **Creds you get**: Plaintext passwords (e.g., database connections).
- **Prerequisites**: File read access (often admin for system dirs).
- **How it works**: Search dirs like C:\inetpub, C:\Program Files: findstr /si password *.config; Manual review.
- **Notes**: Common on servers (IIS/SQL). Not "dumping" but extracting—high value.
---
## 11. Kerberos Ticket Cache
- **What it is**: Stored tickets for SSO (in memory or files).
- **Creds you get**: TGT/TGS tickets for network auth.
- **Prerequisites**: User/admin; tool like Rubeus/Mimikatz.
- **How it works**: Rubeus.exe triage to list; Export: sekurlsa::tickets /export in Mimikatz.
- **Notes**: On domain-joined servers, dumps for cross-machine access.
---
## 12. App-Specific Stores (e.g., PuTTY, WinSCP in AppData)
- **What it is**: Tools store session creds in profiles.
- **Creds you get**: SSH/FTP passwords.
- **Prerequisites**: User access to %APPDATA%.
- **How it works**: For PuTTY: Reg keys HKCU\Software\SimonTatham\PuTTY\Sessions; Decrypt with tools like putty2mimikatz.
- **Notes**: Servers with remote tools—leads to external pivots.
---
## 13. Memory of Other Processes
- **What it is**: Apps holding creds in RAM (e.g., cmd.exe with net use).
- **Creds you get**: Transient plaintext creds.
- **Prerequisites**: Admin; process dump tools.
- **How it works**: Dump process: `procdump.exe -p <pid>`; Strings search or Mimikatz parse.
- **Notes**: Advanced; risky detection. Servers run creds in scripts.
---
## 14. AD-Specific (DCSync on Domain Controllers)
- **What it is**: Replicate domain hashes from DC.
- **Creds you get**: All domain user hashes (e.g., krbtgt).
- **Prerequisites**: Domain Admin or DCSync rights on DC.
- **How it works**: 
```
SafetyKatz.exe "lsadump::dcsync /user:krbtgt /domain:<domain>"
```
- **Notes**: Server-only (DCs); for enterprise escalation.
---
## 15. Trust Keys (on Domain Controllers)
- **What it is**: Keys for domain trusts.
- **Creds you get**: RC4/AES keys for cross-domain auth.
- **Prerequisites**: DA on DC.
- **How it works**: 
```
SafetyKatz.exe "lsadump::trust /patch"
```
- **Notes**: For forest attacks; servers in multi-domain setups.