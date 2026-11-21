ARP Scan with ARP Requests (Discover IPs)

```
nmap -sn <network>
```

---

Get Lists Of Hosts (it will query DNS and slow down the process)

```
nmap -sL 10.10.0-255.55-255 
```
(51456 Hosts)

---

Without DNS Query

```
nmap -sL -n 10.10.0-5.0-56
``` 
(342 Hosts)

---
### Grep command to filter IP Addresses
```
grep -oP '(\d{1,3}\.){3}\d{1,3}' livehosts59-subnet
```