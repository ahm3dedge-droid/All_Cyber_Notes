
#### this Requires Local Admin Privileges

 Disable realtime monitoring:
```
Set-MpPreference -DisableRealtimeMonitoring $true
```
---
```
Set-MpPreference -DisableIOAVProtection $true
```
---

Disable Windows Defender Firewall Domain, Public, Private
```
Set-NetFirewallProfile -Profile Domain,Public,Private -Enabled False
```
---

command to add allow a port on windows firewall to use reverse shells
```
New-NetFirewallRule -DisplayName "Allow Port 8080 Inbound" -Direction Inbound -Action Allow -Protocol TCP -LocalPort 8080
```