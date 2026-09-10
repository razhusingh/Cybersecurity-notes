
# SOC Analyst L1 – Day 16 
## IP/Data Packets + TTL + TCP 3-Way Handshake

---

# 🚀 1. 30-Second Recall

- Packet = Small unit of data sent over a network
- Packet = Header + Payload
- Header = Control Information
- Payload = Actual Data
- Encapsulation = Each network layer adds its header
- Encapsulation Flow = Application → Transport → Network → Data Link
- Packet Example = [Ethernet] [IP] [TCP] [Data]
- IP Header = Layer 3
- IP Header Fields = Version, Source IP, Destination IP, TTL, Protocol, Total Length, Checksum
- TCP Header = Layer 4
- TCP Header Fields = Source Port, Destination Port, Sequence, ACK, Flags, Window Size
- TTL = Packet Lifetime / Hop Limit
- Every Router = TTL − 1
- TTL = 0 → Packet Discarded + ICMP Message
- Ping & Traceroute use TTL-related network behavior
- TCP 3-Way Handshake = SYN → SYN-ACK → ACK
- SYN = Start Connection
- ACK = Confirm
- FIN = Close
- RST = Reset
- PSH = Push Data
- URG = Urgent
- SYN Only / Many SYNs = Possible SYN Flood
- SYN + FIN = Suspicious / Scan
- RST Flood = Disruption
- No ACK = Half-Open Connection Pattern
- 100,000 SYN + 0 ACK → SYN Flood / DDoS

---

# 📌 2. Must Remember

## 📦 IP / Data Packet

A **packet** is a small unit of data transmitted across a network.

```text
Packet
├── Header = Control Information
└── Payload = Actual Data
```

Payload may contain:

- Text
- Images
- Video
- Other transmitted data

---

## 📦 Packet Encapsulation

As data moves down the network stack, each relevant layer adds control information.

```text
Application
    ↓
Transport
    ↓
Network
    ↓
Data Link
```

Example:

```text
[Ethernet] [IP] [TCP] [Data]
```

This process is called **Encapsulation**.

---

# 🌐 IPv4 Header — Layer 3

| Field | Meaning | SOC Use |
|---|---|---|
| Version | IPv4/IPv6 | Protocol identification |
| Source IP | Sender | Identify source |
| Destination IP | Receiver | Identify target |
| TTL | Packet lifetime | Detect anomalies |
| Protocol | TCP/UDP/ICMP | Identify traffic type |
| Total Length | Packet size | Spot unusual transfers |
| Header Checksum | Header integrity | Detect corruption |

### ⭐ Important

**Source IP**
→ Where packet came from

**Destination IP**
→ Where packet is going

**Protocol**
→ TCP / UDP / ICMP etc.

**Total Length**
→ Unusual packet sizes/traffic patterns may help investigation.

---

# 🔢 TCP Header — Layer 4

| Field | Meaning | SOC Use |
|---|---|---|
| Source Port | Sender port | Identify origin |
| Destination Port | Target service | Identify targeted service |
| Sequence Number | Data ordering | Session analysis |
| ACK Number | Confirmation | Flow validation |
| Flags | Connection state | Attack detection |
| Window Size | Flow control | Traffic behaviour |

---

# ⏳ TTL — Time To Live

**TTL = Packet lifetime measured as a hop limit.**

Purpose:

> Prevent packets from circulating indefinitely.

### How It Works

```text
Packet Sent
   ↓
Router → TTL - 1
   ↓
Router → TTL - 1
   ↓
Router → TTL - 1
   ↓
TTL = 0
   ↓
Packet Discarded
   ↓
ICMP Message Returned
```

TTL can help understand:

- Packet path
- Hop behaviour
- Network anomalies

---

## 🔍 TTL + Traceroute

**Traceroute** sends packets with progressively increasing TTL values.

When TTL reaches **0** at a router:

```text
Router
  ↓
Drops Packet
  ↓
Returns ICMP Message
```

This helps reveal successive **network hops** toward the destination.

**Ping and traceroute both involve TTL in network diagnostics.**

---

# 🤝 TCP 3-Way Handshake

Purpose:

> Establish a reliable TCP connection before data transfer.

```text
Client                  Server

SYN  ------------------->
     <---------------- SYN-ACK
ACK  ------------------->

      CONNECTION
      ESTABLISHED
```

### Remember

> **SYN → SYN-ACK → ACK**

---

# 🚩 TCP Flags

| Flag | Meaning | SOC Relevance |
|---|---|---|
| SYN | Start | Connection attempts |
| ACK | Confirm | Established/normal flow |
| FIN | Close | Session termination |
| RST | Reset | Abrupt termination |
| PSH | Push Data | Immediate data delivery |
| URG | Urgent | Rarely seen |

---

# 🚨 Suspicious TCP Patterns

| Pattern | Think |
|---|---|
| Large number of SYNs without completion | SYN Flood |
| SYN + FIN | Suspicious / Scan |
| RST Flood | Disruption |
| No ACK / incomplete handshake | Half-open connection pattern |

> These are **indicators to investigate**, not automatic proof of an attack.

---

# 🛡️ Real SOC Scenario

```text
Source IP: 185.221.x.x
Packets: 100,000 SYN
ACK: 0
Destination: Port 80
```

### Analysis

```text
Huge SYN Volume
      +
No ACK
      +
Target Port 80
      ↓
Possible SYN Flood DDoS
```

SOC analyst should validate the traffic pattern and surrounding evidence before confirming the incident.

---

# 🧠 Quick Packet Analysis

When looking at a packet, quickly identify:

```text
Who sent it?
→ Source IP / Source Port

Where is it going?
→ Destination IP / Destination Port

What traffic?
→ Protocol

How long can it travel?
→ TTL

How large?
→ Total Length

What is TCP doing?
→ Flags
```

---

# 💼 3. Interview Q&A

### Q1. What is a network packet?

**Answer:** A packet is a small unit of data transmitted over a network. It contains a **header and payload**.

---

### Q2. What is the difference between Header and Payload?

**Answer:**

- **Header** = Control information needed to deliver/process the packet
- **Payload** = Actual data being transmitted

---

### Q3. What is packet encapsulation?

**Answer:** Encapsulation is the process where network layers add their own control information as data moves down the network stack.

```text
Application → Transport → Network → Data Link
```

---

### Q4. What are important IPv4 header fields?

**Answer:**

- Version
- Source IP
- Destination IP
- TTL
- Protocol
- Total Length
- Header Checksum

---

### Q5. What are important TCP header fields?

**Answer:**

- Source Port
- Destination Port
- Sequence Number
- ACK Number
- Flags
- Window Size

---

### Q6. What is TTL?

**Answer:** TTL (Time To Live) is a hop limit that prevents an IP packet from circulating indefinitely.

Each router decreases TTL by **1**.

---

### Q7. What happens when TTL becomes 0?

**Answer:** The router discards the packet and normally sends an **ICMP Time Exceeded** message to the source.

---

### Q8. How does traceroute use TTL?

**Answer:** Traceroute sends packets with increasing TTL values. Routers where TTL expires return ICMP responses, helping reveal the hops toward the destination.

---

### Q9. What is the TCP 3-Way Handshake?

**Answer:**

```text
Client → SYN
Server → SYN-ACK
Client → ACK
```

After this, the TCP connection is established.

---

### Q10. What are the important TCP flags?

**Answer:**

- SYN = Start
- ACK = Confirm
- FIN = Close
- RST = Reset
- PSH = Push Data
- URG = Urgent

---

### Q11. What can indicate a SYN Flood?

**Answer:** A very large number of **SYN packets without completed handshakes/ACKs** can indicate a SYN Flood.

---

### Q12. Why are TCP flags important to a SOC Analyst?

**Answer:** TCP flag patterns help identify connection behaviour, scans, incomplete connections, resets and possible attacks such as SYN floods.

---

# 🛡️ 4. SOC Analyst Mindset

**Understand this flow — don't memorise it word-for-word.**

```text
Network Alert
      ↓
Check Source → Destination
      ↓
Check IPs + Ports
      ↓
Identify Protocol
      ↓
Check Packet Size / TTL
      ↓
For TCP → Check Flags
      ↓
Is Handshake Normal?
      ↓
Look for Abnormal Pattern
      ↓
Correlate Traffic
      ↓
Benign / Escalate
```

## Quick SOC Thinking

### Source & Destination

```text
Source IP
→ Who initiated the traffic?

Destination IP
→ Who is being targeted/contacted?
```

### Ports

```text
Source Port
→ Origin-side port

Destination Port
→ Target service
```

### Protocol

```text
TCP / UDP / ICMP
→ What type of traffic?
```

### TTL

Unusual TTL behaviour can be another clue during packet/network analysis.

### TCP Flags

```text
SYN → Connection attempt
ACK → Confirmation
FIN → Normal close
RST → Reset
```

Repeated or abnormal flag patterns deserve investigation.

---

## 🚨 SYN Flood Thinking

Example:

```text
Source: External IP
Destination: Web Server
Port: 80
SYN: 100,000
ACK: 0
```

Think:

```text
Huge SYN Volume
      ↓
Connections Not Completing
      ↓
Many Half-Open Connections
      ↓
Possible SYN Flood DDoS
```

Don't confirm an attack from one packet alone. Validate the **volume, timing, sources and surrounding traffic**.

---

# 📝 5. Question Paper Mode

1. What is an IP/data packet?
2. Differentiate between packet Header and Payload.
3. What is packet encapsulation?
4. What happens to data as it moves through Application → Transport → Network → Data Link?
5. Name the important IPv4 header fields and their basic purposes.
6. How can Source IP, Destination IP, Protocol, TTL and Total Length help a SOC Analyst?
7. Name the important TCP header fields.
8. What are Sequence Number, ACK Number, TCP Flags and Window Size used for?
9. What is TTL and why is it required?
10. What happens to TTL at every router, and what happens when it reaches 0?
11. How does traceroute use TTL and ICMP responses?
12. Explain the TCP 3-Way Handshake.
13. Explain SYN, ACK, FIN, RST, PSH and URG flags.
14. Why are TCP flags useful during SOC investigation?
15. What could a large number of SYN packets without completed handshakes indicate?
16. What can SYN + FIN, an RST flood and incomplete/no-ACK handshakes indicate?
17. A source sends 100,000 SYN packets, receives/completes no ACKs and targets port 80. What attack would you suspect?

---

# ✅ 6. Answer Key

**1.** A small unit of data transmitted over a network containing control information and actual data.

**2.**

- Header = Control information
- Payload = Actual transmitted data

**3.** The process of adding protocol/layer information as data moves down the network stack.

**4.** Each relevant layer adds its own header/control information.

Example:

```text
[Ethernet] [IP] [TCP] [Data]
```

**5.**

- Version → IP version
- Source IP → Sender
- Destination IP → Receiver
- TTL → Hop limit
- Protocol → TCP/UDP/ICMP etc.
- Total Length → Packet size
- Header Checksum → IPv4 header integrity

**6.**

- Source IP → Identify source
- Destination IP → Identify target
- Protocol → Traffic type
- TTL → Detect/understand anomalies and path behaviour
- Total Length → Identify unusual packet/transfer patterns

**7.**

- Source Port
- Destination Port
- Sequence Number
- ACK Number
- Flags
- Window Size

**8.**

- Sequence Number → Data ordering
- ACK Number → Confirmation
- Flags → Connection state/control
- Window Size → Flow control

**9.** TTL is a hop limit that prevents packets from circulating indefinitely.

**10.** Every router decreases TTL by 1. At TTL 0, the packet is discarded and an ICMP Time Exceeded response is normally returned.

**11.** Traceroute uses progressively increasing TTL values; TTL expiration at successive routers generates responses that reveal network hops.

**12.**

```text
SYN → SYN-ACK → ACK
```

This establishes a TCP connection.

**13.**

- SYN → Start connection
- ACK → Confirm
- FIN → Close
- RST → Reset
- PSH → Push data
- URG → Urgent data

**14.** They reveal TCP connection behaviour and can help identify abnormal connections, scans, resets and attack patterns.

**15.** Possible **SYN Flood / half-open connection attack pattern**.

**16.**

- SYN + FIN → Suspicious / possible scan
- RST Flood → Possible disruption
- Incomplete/no-ACK handshakes → Possible half-open attack pattern

**17.** Suspect a **SYN Flood DDoS** and validate with surrounding network evidence.

---
