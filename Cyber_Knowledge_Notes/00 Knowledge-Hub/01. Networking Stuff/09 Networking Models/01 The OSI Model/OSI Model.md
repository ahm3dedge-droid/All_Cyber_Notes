This is conceptual model, developed by the ISO (International Organization of Standardization).

7 Layers of OSI Model are:

| **Layer Number** | **Layer Name**     | **Main Function**                                                                    | **Example Protocols and Standards**       |
| ---------------- | ------------------ | ------------------------------------------------------------------------------------ | ----------------------------------------- |
| Layer 7          | Application layer  | Providing services and interfaces to applications                                    | RADIUS, HTTP, FTP, DNS, POP3, SMTP, IMAP  |
| Layer 6          | Presentation layer | Data encoding, encryption, and compression                                           | Unicode, MIME, JPEG, PNG, MPEG            |
| Layer 5          | Session layer      | Establishing, maintaining, and synchronising sessions                                | NFS, RPC                                  |
| Layer 4          | Transport layer    | End-to-end communication and data segmentation                                       | UDP, TCP                                  |
| Layer 3          | Network layer      | Logical addressing and routing between networks                                      | IP, ICMP, IPSec                           |
| Layer 2          | Data link layer    | Reliable data transfer between adjacent nodes                                        | Ethernet (802.3), WiFi (802.11)           |
| Layer 1          | Physical layer     | Physical data transmission media, Wires, Data travels in 0's and 1's, Antennas used. | Electrical, optical, and wireless signals |

> Remembering the OSI model layers with their layer numbers is important; otherwise, you will struggle to understand terms such as “layer 3 switch” or “layer 7 firewall.”

![[Pasted image 20251230024338.png]]

### Layer 1. Physical
The Physical Layer, i.e., layer 1, defines the medium to transfer the data, data travels in 0's and 1's.

### Layer 2. Data Link (MAC Addresses)
 The data link layer, i.e., layer 2, represents the protocol that enables data transfer between nodes on the same network segment.

### Layer 3. Network (IP Addresses)
This layer basically defines the IP addressing in the network. it is responsible for routing the data across complex networks.

###### Layer 2 and Layer 3 Switches difference.
![[Pasted image 20251230110813.png]]

### Layer 4. Transport
This layer defines and decides which protocol to use either TCP or UDP.
it enables end-to-end communication between running applications on different hosts. Support various functions like flow control, segmentation, and error correction.

TCP 3 way handshake comes in it.
TCP flags comes in this layer

**TCP Segments are in the IP Packets**
![[Pasted image 20251230112118.png]]

### Layer 5. Session
this layer is responsible for creating and establishing, maintaining, closing a connection between client and server.
*Examples of the session layer are Network File System (NFS) and Remote Procedure Call (RPC).*
this session layer is just responsible for keeping the connection open.

**Popular Protocols at Session Layer:**
- L2TP
- RTCP
- H.245
- SOCKS

### Layer 6. Presentation
this layer is basically responsible for Data Format and Encryption.
data format means simply file types (PDF, HTML, PNG, JPEG)
**SSL** operates at this layer 6

### Layer 7. Application
This layer is the top layer, the user interacts with applications like YouTube on this layer. 
The protocols are:
- HTTP
- FTP
- DNS
- SMTP
- POP3
- IMAP 


