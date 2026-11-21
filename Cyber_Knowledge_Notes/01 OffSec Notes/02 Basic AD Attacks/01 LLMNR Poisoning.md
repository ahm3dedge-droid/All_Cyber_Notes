LLMNR Poisoning

LLMNR ( Link Local Multi-cast Name Resolution ) is a network protocol which is enabled by default on networks, this helps us to identify hosts on a local network.
in this attack all the clients on the network can listen and respond to the LLMNR broadcast messages request, so when a victim broadcast the LLMNR message and the server or DNS fails to locate that, then the attacker say, “hey i know this”, please share your hash and I'll get you connected.  so the user shares his password hash and then we can crack that hash to obtain a password.
we can use tools like hashcat and johnthripper to crack that hash. 
we use a tool called responder to query hosts and get hashes.

___
## Process of Attack

1. Start the Responder Tool:
   Launch the Responder tool to begin capturing network traffic and hashes.
```
sudo responder -I eth0 -dwDv
```

2. Responder Intercepts Authentication Requests:
When a user requests a network resource that the DNS server cannot locate, Responder intercepts the request and responds, pretending to know the location of the resource.

3. Capture NTLMv2 Hashes:
The user's system, believing Responder's response, sends the NTLMv2 hash of the user's password to Responder.
______ 
**Responder Command**

```
sudo responder -I eth0 -dwDv
```

---

# **Mitigation**

### 1. Disable the Multicast Name Resolution (LLMNR will be mitigated)
first enable this GPO 
Computer Configuration > Policies > Administrative Templates > Network > DNS Client > "turn off the multicast name resolution" 
![[Pasted image 20251219193910.png]]
### Disable NBT-NS via Registry
Open the registry by typing Regedit in the run dialogue. Navigate to registry key at the following location.
Computer\HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Services\NetBT\Parameters\Interfaces\
From here, we’ll be presented with multiple keys, each represents a network interface. You’ll want to adjust the NetbiosOptions value on each from the default of zero, to a value of 2.\

_________________________

run these command in the powershell
$regkey = "HKLM:SYSTEM\CurrentControlSet\services\NetBT\Parameters\Interfaces"
	
```
Get-ChildItem $regkey |foreach { Set-ItemProperty -Path "$regkey\$($_.pschildname)" -Name NetbiosOptions -Value 2 -Verbose}
```

OR

To disable NBT-NS via GPO, we can simply write a PowerShell script (see below) and save it in Startup Scripts.
```
set-ItemProperty -Path HKLM:\SYSTEM\CurrentControlSet\services\NetBT\Parameters\Interfaces\tcpip* -Name NetbiosOptions -Value 2
```
_________________________
# To disable MDNS:
 ***Go to the group policy editor and create a new GPO (group policy object)***

• Create the new GPO.
• Go to: Computer Configuration -> Preferences -> Windows Settings -> Registry
• Right click the right panel -> New -> Registry Item
• Action: Update
• Hive: HKEY_LOCAL_MACHINE
• Key Path: SYSTEM\CurrentControlSet\Services\Dnscache\Parameters
• Value name: EnableMDNS
• Value type: DWord
• Value data: 0

![[Pasted image 20251219193721.png]]

---
---
# **Manual Toggle (mitigation of poisoning)** 
MDNS, LLMNR, NBT-NS
### **1. Local Link Muilticast Name Resolution**

Registiry Key PATH =`   ### SOFTWARE\Policies\Microsoft\Windows NT\DNSClient\EnableMulticast   `

Enable = 1

Disable = 0

### **2. MDNS**
To disable NBT-NS, navigate to Network Connections > Network Adapter Properties > TCP/IPv4 Properties > Advanced tab > WINS tab and select “Disable NetBIOS over TCP/IP.”

Registery Key PATH:
`Computer\HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Services\NetBT\Parameters\Interfaces\tcp*`
Default = 0
Disable Value = 2

### **3. SMB Signing**

Disable SMB Signing for the Server: Run the following commands

```
Set-ItemProperty -Path "HKLM:\\SYSTEM\\CurrentControlSet\\Services\\LanmanServer\\Parameters" -Name "RequireSecuritySignature" -Value 0
```

Disable SMB Signing for the Client: Run the following commands

```
Set-ItemProperty -Path "HKLM:\\SYSTEM\\CurrentControlSet\\Services\\LanmanWorkstation\\Parameters" -Name "EnableSecuritySignature" -Value 0
```

```
Set-ItemProperty -Path "HKLM:\\SYSTEM\\CurrentControlSet\\Services\\LanmanWorkstation\\Parameters" -Name "RequireSecuritySignature" -Value 0
```