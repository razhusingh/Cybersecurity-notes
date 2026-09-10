# SOC Analyst L1 – Day 13 | Reply 1
OSI Model + TCP/IP Model
#  30-Second Recall
- OSI = Open Systems Interconnection

- OSI = 7-layer conceptual model

- L7 Application = HTTP/HTTPS, FTP, SMTP → User-facing network services

- L6 Presentation = Formatting, Encryption/Decryption, Encoding

- L5 Session = Establish, Manage & Terminate Sessions

- L4 Transport = TCP/UDP, Ports, End-to-End Communication

- L3 Network = IP Addressing + Routing

- L2 Data Link = MAC + Local Network Delivery

- L1 Physical = Cables, Signals, Hardware Transmission

- Encapsulation = Sender: Layer 7 → Layer 1, information added as data moves down

- Decapsulation = Receiver: Layer 1 → Layer 7, information removed as data moves up

- TCP = Reliable; UDP = Faster but no delivery guarantee

- TCP/IP = Practical model used by real networks/Internet

- TCP/IP standard model = 4 Layers: Application → Transport → Internet → Network Access

- TCP/IP Application = OSI 7 + 6 + 5

- TCP/IP Transport = OSI 4

- TCP/IP Internet = OSI 3

- TCP/IP Network Access = OSI 2 + 1

- Port Issue → Transport

- IP Issue → Network/Internet

- DNS Issue → Application

- ARP/MAC Issue → Data Link/Network Access

- OSI = Mainly conceptual/reference model; TCP/IP = Real-world protocol suite/model

#  Must Remember Points
OSI Model
- The OSI (Open Systems Interconnection) Model is a 7-layer framework used to understand how network communication works from one system to another.

7 Layers - top to bottom
| Layer | Name         | Main Job                          | Examples               |
| ----- | ------------ | --------------------------------- | ---------------------- |
| 7     | Application  | Network services to applications  | HTTP, HTTPS, FTP, SMTP |
| 6     | Presentation | Format, encrypt, encode, compress | TLS/SSL, Encoding      |
| 5     | Session      | Manage communication sessions     | Login session          |
| 4     | Transport    | End-to-end transport              | TCP, UDP               |
| 3     | Network      | Routing & logical addressing      | IP, Router             |
| 2     | Data Link    | Local delivery & MAC addressing   | MAC, Ethernet          |
| 1     | Physical     | Raw-bit transmission              | Cables, Signals        |

Memory Trick
- A P S T N D P
- All People Seem To Need Data Processing

7️⃣ Application Layer
Purpose
- Closest to user/application
- Provides network services used by software
- Web browsing, email, file transfer

Protocols
- HTTP / HTTPS
- FTP
- SMTP

SOC Perspective
- Phishing
- Malicious URLs
- Suspicious API Calls

6️⃣ Presentation Layer
Purpose
- Data Formatting
- Translation/Encoding
- Encryption / Decryption
- Compression

Examples
- TLS/SSL
- Character Encoding

SOC Perspective
- Encryption Analysis
- SSL Stripping / MITM

5️⃣ Session Layer
Purpose
- Establishes → Manages → Terminates communication sessions.

Examples
- Login Sessions
- Session-related communication

SOC Perspective
- Session Hijacking
- Token Reuse

4️⃣ Transport Layer ⭐
Purpose
- End-to-End Communication
- Segmentation
- Reliability/Flow Control where applicable
- Uses Ports

TCP
- Connection-oriented
- Reliable
- Ordered delivery

UDP
- Connectionless
- Lower overhead/faster
- No guarantee of delivery/order

SOC Perspective
- Port Scanning
- SYN Flood
- Suspicious Ports
- Traffic Anomalies

3️⃣ Network Layer ⭐
Purpose
- IP Addressing
- Routing
- Finds path between networks

Protocol
- IPv4 / IPv6

Device
- Router

SOC Perspective
- Suspicious IPs
- External Connections
- IP Tracking
- Geolocation
- Botnet Traffic

2️⃣ Data Link Layer ⭐
Purpose
- MAC Address Communication
- Local Network Delivery
- Framing

Examples
- MAC
- Ethernet

SOC Perspective
- ARP Spoofing
- MAC Anomalies
- Internal Network Attacks

1️⃣ Physical Layer
Purpose
- Transmits raw bits (1s and 0s)
- Physical/electrical/optical/wireless signalling

Examples
- Cables
- Fibre
- Wireless Signals
- Network Hardware

SOC Perspective
- Rarely investigated directly by L1 SOC
- Relevant to physical/hardware attacks

# 📦 Encapsulation & Decapsulation

Encapsulation — Sender
```
Application (7)
      ↓
Presentation (6)
      ↓
Session (5)
      ↓
Transport (4)
      ↓
Network (3)
      ↓
Data Link (2)
      ↓
Physical (1)
      ↓
   Network

```
As data moves downward, layers add the control information needed for communication.

Decapsulation — Receiver
```
   Network
      ↓
Physical (1)
      ↓
Data Link (2)
      ↓
Network (3)
      ↓
Transport (4)
      ↓
Session (5)
      ↓
Presentation (6)
      ↓
Application (7)
```
Receiver removes the corresponding information while moving upward until the original application data is delivered.

Remember:

- Sender = Encapsulation ↓
- Receiver = Decapsulation ↑

# 🌐 TCP/IP Model
- TCP/IP is the model/protocol suite used for real-world Internet communication. The PDF primarily teaches the 4-layer TCP/IP model.

4 TCP/IP Layers
| TCP/IP         | Maps to OSI   |
| -------------- | ------------- |
| Application    | OSI 7 + 6 + 5 |
| Transport      | OSI 4         |
| Internet       | OSI 3         |
| Network Access | OSI 2 + 1     |

Easy mapping
```
OSI                         TCP/IP

7 Application ┐
6 Presentation ├──────────► Application
5 Session      ┘

4 Transport ──────────────► Transport

3 Network ────────────────► Internet

2 Data Link    ┐
1 Physical     ┴──────────► Network Access

```
# TCP/IP Application Layer
Includes:
- HTTP / HTTPS
- DNS
- FTP

SOC
- Phishing
- DNS Attacks
- API Abuse

# TCP/IP Transport Layer
Protocols:
- TCP
- UDP

SOC
- Port Scanning
- SYN Flood
- Traffic Anomalies

# TCP/IP Internet Layer
Protocol:
- IP

SOC
- Suspicious IP
- External Communication
- Botnet Traffic

# TCP/IP Network Access Layer
Includes:
- MAC
- ARP
- Ethernet

SOC
- ARP Spoofing
- Internal Network Attacks

# OSI vs TCP/IP| Feature       | OSI                                    | TCP/IP                               |
| ------------- | -------------------------------------- | ------------------------------------ |
| Layers        | 7                                      | Commonly taught as 4                 |
| Nature        | Reference/conceptual model             | Practical protocol suite/model       |
| Real Internet | Used for understanding/troubleshooting | TCP/IP protocols power real networks |

🛡️ SOC Layer Mapping
```
When you see a security event, identify the relevant layer:

Port issue
→ Transport Layer

IP issue
→ Network / Internet Layer

DNS issue
→ Application Layer

ARP/MAC issue
→ Data Link / Network Access Layer

Example from page 20:

Suspicious HTTPS login from unknown external IP

Think:

HTTPS/Application → TCP/443 Transport → External IP Network → Local Network Data Link.
```
# Interview Q&A
Q1. What is the OSI Model?
- Answer: OSI (Open Systems Interconnection) is a 7-layer reference model that explains how data travels between systems over a network.

Q2. Name the 7 OSI layers.
- Answer: Application → Presentation → Session → Transport → Network → Data Link → Physical
Memory: A P S T N D P

Q3. What does the Application Layer do?
- Answer: It provides network services to applications/end users.
Examples: HTTP/HTTPS, FTP, SMTP

Q4. What does the Presentation Layer do?
- Answer: It handles data formatting, encoding, compression and encryption/decryption.

Q5. What does the Session Layer do?
- Answer: It establishes, manages and terminates sessions between communicating systems.

Q6. What does the Transport Layer do?
- Answer: It provides end-to-end communication using protocols such as TCP and UDP.

Q7. What is the difference between TCP and UDP?
- Answer: TCP: Connection-oriented, reliable, ordered delivery.
UDP: Connectionless, lower overhead, no guarantee of delivery/order.

Q8. What does the Network Layer do?
- Answer: It handles logical IP addressing and routing between networks.

Q9. What does the Data Link Layer do?
- Answer: It handles local network delivery, framing and MAC addressing.

Q10. What does the Physical Layer do?
- Answer: It transmits raw bits (1s and 0s) through physical/electrical/optical/wireless media.

Q11. What is Encapsulation?
- Answer: On the sender side, data moves down the network stack, with protocol information added as required by each layer.

Q12. What is Decapsulation?
- Answer: On the receiver side, data moves up the stack, with corresponding protocol information removed until the original data reaches the application.

Q13. What is the TCP/IP Model?
- Answer: TCP/IP is the practical networking model/protocol suite used by real networks and the Internet.

Q14. Name the 4 TCP/IP layers.
- Answer: Application → Transport → Internet → Network Access

Q15. How does TCP/IP map to OSI?
Answer:
- TCP/IP Application = OSI 7, 6, 5
- TCP/IP Transport = OSI 4
- TCP/IP Internet = OSI 3
- TCP/IP Network Access = OSI 2, 1

Q16. OSI vs TCP/IP?

Answer:
- OSI: 7-layer reference/conceptual model.
- TCP/IP: Commonly represented as a 4-layer practical model/protocol suite used on real networks.

# SOC Analyst Mindset
Whenever you see a network alert/log:
```
Security Alert
      ↓
What is suspicious?
      ↓
Identify Protocol / Address / Port
      ↓
Which Network Layer?
      ↓
Check Relevant Logs
      ↓
Correlate Activity
      ↓
Determine Malicious / Benign
      ↓
Escalate / Close
```
Quick SOC Thinking
```
Malicious URL / Phishing / DNS
→ Application

SSL/TLS issue
→ Presentation conceptually

Session Hijacking / Token Reuse
→ Session conceptually

Port Scan / SYN Flood / Port issue
→ Transport

Suspicious IP / Routing
→ Network / Internet

ARP Spoofing / MAC anomaly
→ Data Link / Network Access

Physical hardware issue/attack
→ Physical

Example

Alert:

Suspicious HTTPS login from unknown external IP

Think:
HTTPS
→ Application

TCP / Port 443
→ Transport

External IP
→ Network

MAC / Local Delivery
→ Data Link
```
# Question Paper Mode

1. What is the OSI Model?

2. Name all 7 OSI layers in order.

3. What does the Application Layer do? Give protocol examples.

4. What are the functions of the Presentation Layer?

5. What does the Session Layer do?

6. What does the Transport Layer do?

7. Differentiate TCP and UDP.

8. What does the Network Layer do?

9. What does the Data Link Layer do?

10. What does the Physical Layer do?

11. What is Encapsulation and in which direction does it occur?

12. What is Decapsulation and in which direction does it occur?

13. What is the TCP/IP Model?

14. Name the 4 TCP/IP layers.

15. Map the TCP/IP layers to the OSI layers.

16. Differentiate OSI and TCP/IP.

17. Which layer would you investigate for a port scan or SYN flood?

18. Which layer would you associate with suspicious IP communication?

19. Which layer would you associate with ARP spoofing or MAC anomalies?

20. Which layer would you associate with phishing, DNS attacks and malicious URLs?

21. In a suspicious HTTPS login from an unknown IP, how would you break the activity into network layers?




# Answer Key

1. A 7-layer reference framework explaining network communication.

2. Application → Presentation → Session → Transport → Network → Data Link → Physical

3. Provides network services to applications/users. Examples: HTTP/HTTPS, FTP, SMTP.

4. Formatting, translation/encoding, compression and encryption/decryption.

5. Establishes, manages and terminates communication sessions.

6. Provides end-to-end transport; associated with protocols such as TCP and UDP and port-based communication.

7.
- TCP = Connection-oriented, reliable and ordered.
- UDP = Connectionless, lower overhead and no delivery/order guarantee.

8. Handles IP addressing and routing between networks.

9. Handles MAC addressing, framing and local network delivery.

10. Transmits raw bits through physical/electrical/optical/wireless media.

11. Encapsulation occurs as sender data moves down the stack (7 → 1) and protocol information is added.

12. Decapsulation occurs as received data moves up the stack (1 → 7) and protocol information is removed.

13. The practical networking model/protocol suite used by the Internet and real networks.

14. Application → Transport → Internet → Network Access

15.
- Application = OSI 7 + 6 + 5
- Transport = OSI 4
- Internet = OSI 3
- Network Access = OSI 2 + 1

16.
- OSI = 7 layers, reference/conceptual.
- TCP/IP = commonly 4 layers, practical and used for real Internet networking.

17. Transport Layer (Layer 4).

18. Network Layer (Layer 3) / TCP-IP Internet Layer.

19. Data Link Layer (Layer 2) / TCP-IP Network Access.

20. Application Layer.

21.
- HTTPS → Application
- TCP/443 → Transport
- External IP → Network
- Local MAC/network delivery → Data Link