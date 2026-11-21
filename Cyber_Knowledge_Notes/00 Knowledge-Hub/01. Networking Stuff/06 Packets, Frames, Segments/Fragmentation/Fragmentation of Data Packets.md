## What Is Fragmentation in Networking?
- Fragmentation is a process that occurs when a sending device needs to transmit a data packet that is larger than the Maximum Transmission Unit (MTU) supported by the network.
- In this case, the device splits the original packet into smaller fragments, each sized to fit within the allowed MTU. Each fragment is sent separately.
- An offset value is included with each fragment. This offset tells the receiving device the correct order in which the fragments should be reassembled to reconstruct the original packet.

![[Pasted image 20260124093731.png]]