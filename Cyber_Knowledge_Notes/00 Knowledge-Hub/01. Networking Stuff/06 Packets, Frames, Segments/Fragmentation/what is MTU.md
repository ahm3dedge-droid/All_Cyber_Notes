## (MTU) Maximum Transmission Unit
The (MTU) Maximum Transmission Unit is the maximum size of Data in bytes that your network adapter can send In an unfragmented unit. 

---
**here is what happen, if MTU is 750** 
the 1600 Bytes data will be fragmented into 3 fragments

![[Pasted image 20260123112445.png]]

---

Command to see MTU on windows CMD
```
netsh interface ipv4 show interfaces
```

![[Pasted image 20260123112816.png]]