# Day 16 - IP/Data Packets, TTL & TCP 3-Way Handshake

---

# IP/Data Packets

## What is an IP Packet?

A packet is a small unit of data sent over a network.

- Data is broken into packets before transmission.
- Packets are transmitted between devices and reassembled at the destination.
- Every packet follows a specific structure defined by a protocol.
- An IP packet contains:
  - Source and Destination IP addresses
  - Control information
  - Actual data being transmitted

---

# Packet Structure

Every packet contains:

```text
[ Header ] + [ Payload ]
```

### Header
Contains control information required to deliver and process the packet.

Examples:
- Source IP
- Destination IP
- TTL
- Packet Length
- Protocol information

### Payload
Contains the actual data being transmitted.

Examples:
- Text
- Images
- Videos
- Files

---

# Packet Encapsulation

As data moves through network layers, each layer adds its own header.

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
[ Ethernet ] [ IP ] [ TCP ] [ Data ]
```

This process is called **Encapsulation**.

---

# Structure of an IP Packet

Important IP header fields:

## Version
- Identifies the IP version.
- Example: IPv4 or IPv6.

## Total Length
- Specifies the total size of the packet.
- Includes Header + Payload.

## Protocol
Identifies the higher-layer protocol being carried.

Examples:
- TCP
- UDP
- ICMP

## TTL (Time To Live)
- Defines how long/how many hops a packet can travel.
- Each router decreases TTL by 1.
- When TTL reaches 0, the packet is discarded.
- Prevents packets from circulating indefinitely.

## Source IP Address
- IP address of the sender.

## Destination IP Address
- IP address of the intended receiver.
- Routers use it to forward the packet toward its destination.

---

# IPv4 Header Fields - Layer 3

| Field | Meaning | SOC Use |
|---|---|---|
| Version | IPv4 or IPv6 | Protocol identification |
| Source IP | Sender | Identify source/attacker |
| Destination IP | Receiver | Identify target system |
| TTL | Packet lifetime | Detect anomalies |
| Protocol | TCP/UDP/ICMP | Identify traffic type |
| Total Length | Packet size | Detect unusual/exfiltration traffic |
| Header Checksum | Integrity | Detect corruption |

---

# TCP Header - Layer 4

| Field | Meaning | SOC Use |
|---|---|---|
| Source Port | Sender Port | Identify origin |
| Destination Port | Target Service | Detect targeted service/attack |
| Sequence Number | Order Tracking | Session analysis |
| ACK Number | Confirmation | Flow validation |
| Flags | Connection State | Attack detection |
| Window Size | Flow Control | Analyze traffic behavior |

---

# Example Packet

```text
Source IP      : 192.168.1.10
Destination IP : 45.77.123.66
Protocol       : TCP
TTL            : 64
Length         : 1500 Bytes
```

## SOC Analysis

### Source IP
- Internal → May be normal
- Unexpected external source → Investigate

### Destination IP
- Known service → Usually expected
- Unknown/Malicious destination → Alert and investigate

---

# TTL - Time To Live

## What is TTL?

TTL (Time To Live) determines how many **hops** a packet can travel through a network before being discarded.

Its main purpose is to prevent packets from circulating indefinitely.

TTL is also used in other contexts such as:

- DNS caching
- CDN caching

---

# How TTL Works

Each packet contains a numerical TTL value.

```text
Packet Created
     ↓
TTL = Initial Value
     ↓
Router 1 → TTL - 1
     ↓
Router 2 → TTL - 1
     ↓
Router 3 → TTL - 1
```

Every router that forwards the packet decreases TTL by **1**.

If:

```text
TTL = 0
```

the router:

1. Discards the packet.
2. Sends an ICMP message back to the originating host.

This prevents packets from endlessly circulating through the network.

---

# TTL with Ping and Traceroute

Commands such as:

```bash
ping
traceroute
```

use TTL.

## Traceroute

Traceroute sends packets with gradually increasing TTL values.

Example:

```text
TTL 1 → First Router
TTL 2 → Second Router
TTL 3 → Third Router
...
```

When TTL reaches 0 at a router:

- The router discards the packet.
- An ICMP message is returned.

This allows traceroute to identify the routers/hops along the path to a destination.

---

# TCP 3-Way Handshake

## What is the TCP 3-Way Handshake?

The TCP 3-Way Handshake establishes a reliable TCP connection between a client and server before data is transferred.

The process uses three steps:

```text
Client                     Server

   SYN  -------------------->

        <---------------- SYN-ACK

   ACK  -------------------->

        Connection Established
```

### Step 1 - SYN

```text
Client → SYN → Server
```

The client requests a connection.

### Step 2 - SYN-ACK

```text
Server → SYN-ACK → Client
```

The server acknowledges the request and agrees to establish the connection.

### Step 3 - ACK

```text
Client → ACK → Server
```

The client confirms.

The TCP connection is now established.

---

# TCP Flags

| Flag | Meaning | SOC Use |
|---|---|---|
| SYN | Start | Connection attempts |
| ACK | Confirm | Normal established traffic |
| FIN | Close | Session end |
| RST | Reset | Abnormal/forced termination |
| PSH | Push Data | Immediate data delivery |
| URG | Urgent | Rare traffic |

### Normal TCP Connection

```text
Client → SYN
Server → SYN-ACK
Client → ACK

Connection Established
```

---

# Suspicious TCP Patterns for SOC

| Pattern | Possible Meaning |
|---|---|
| SYN Only | SYN Flood |
| SYN + FIN | Suspicious / Scan |
| RST Flood | Disruption |
| No ACK | Half-Open Connection/Attack |

---

# SYN Flood

A SYN Flood abuses the TCP 3-Way Handshake.

Normal:

```text
Client → SYN
Server → SYN-ACK
Client → ACK
```

During a SYN Flood:

```text
Attacker → SYN
Server   → SYN-ACK
Attacker → No ACK
```

The attacker sends a very large number of SYN requests without completing the handshake.

This creates many **half-open connections** and can consume server resources.

---

# Real SOC Scenario

```text
Source IP  : 185.221.x.x
Packets    : 100,000 SYN
ACK        : 0
Destination: Port 80
```

### Analysis

```text
100,000 SYN packets
        +
0 ACK packets
        +
Port 80 (HTTP)
        ↓
Large number of incomplete TCP handshakes
        ↓
SYN Flood
```

### Conclusion

**SYN Flood DDoS Attack**

---