# Day 15 - IP Addressing & MAC Address

---

# IP Addressing

## What is an IP Address?

- An IP address is a unique identifier for a device on a network.
- IP = Device Identity + Location on Network

**Example:**

```text
192.168.1.10
```

---

# IPv4

- IPv4 = 32 bits
- Divided into 4 octets
- Each octet = 8 bits
- Each octet range = 0–255

**Example:**

```text
192.168.1.10
```

### Binary Concept

```text
192 → 11000000
168 → 10101000
```

> SOC doesn't use binary daily, but understanding it helps in subnetting.

---

# IPv4 Structure

```text
192 . 168 . 1 . 10
  |     |    |    |
  8     8    8    8 bits
```

- Total = 32 bits
- 4 Octets
- Each Octet = 1 Byte

---

# Network Part

- Identifies which network the device belongs to.
- Think of it like the **City / Area** in an address.

**Example:**

```text
192.168.1.10

Network Part → 192.168.1
```

This means:

```text
192.168.1.X
```

devices are in the same network.

---

# Host Part

- Identifies the specific device inside the network.
- Think of it like the **House Number** in a city.

**Example:**

```text
192.168.1.10

Host Part → 10
```

This means:

```text
Device number 10 in that network
```

---

# Subnetting Basics

## What is Subnetting?

Subnetting = Dividing a network into smaller networks.

### Why?

- Better Security
- Better Performance
- Easier Management

---

# CIDR Notation

**Example:**

```text
192.168.1.0/24
```

`/24` means:

```text
24 bits = Network
8 bits  = Hosts
```

---

# What is CIDR?

CIDR = Classless Inter-Domain Routing

CIDR improves IP address management by allowing:

- More flexible subnetting
- Efficient IP allocation
- Reduced IP address waste

Organizations use CIDR to allocate IP addresses flexibly and efficiently.

---

# What is a /24 Subnet?

In a `/24` subnet:

```text
24 bits → Network portion
8 bits  → Host portion
```

Subnet masks define how an IP address is divided into:

```text
Network + Host
```

This determines the number of IP addresses available in the range.

---

# How Many IP Addresses in a /24 Subnet?

A `/24` subnet provides **256 total IP addresses**.

### Formula

```text
Total IPs = 2^(32 - subnet prefix)

Total IPs = 2^(32 - 24)

           = 2^8

           = 256
```

### Reserved IPs

Two IPs are reserved:

#### Network Address
- First IP address.
- Identifies the subnet itself.

Example:

```text
192.168.0.0
```

#### Broadcast Address
- Last IP address.
- Used to communicate with all hosts in the subnet.

Example:

```text
192.168.0.255
```

### Usable IPs

```text
256 - 2 = 254
```

A `/24` subnet has:

```text
254 usable IP addresses
```

---

# Common Subnets

| CIDR | Subnet Mask | Hosts |
|------|-------------|------:|
| /24 | 255.255.255.0 | 254 |
| /16 | 255.255.0.0 | 65,534 |
| /8  | 255.0.0.0 | 16M |

---

# Versions of IP Addresses

## IPv4 (Internet Protocol Version 4)

- Address Size: 32-bit
- Format: Decimal
- Example: `192.168.1.1`
- Total Addresses: 4,294,967,296
- IPSec: Optional
- Widely used but facing address exhaustion

## IPv6 (Internet Protocol Version 6)

- Address Size: 128-bit
- Format: Hexadecimal
- Example: `2001:db8::1`
- Total Addresses: 3.4 × 10³⁸
- IPSec: Mandatory
- Designed to solve IPv4 address shortage

---

# Classes of IP Addresses

## Class A

- Range: `1.0.0.0 – 126.255.255.255`
- Network Bits: 8
- Host Bits: 24
- Use: Large Networks
- Example: Government Organizations
- `127` is reserved for Loopback

---

## Class B

- Range: `128.0.0.0 – 191.255.255.255`
- Network Bits: 16
- Host Bits: 16
- Use: Medium-sized Networks
- Example: Universities

---

## Class C

- Range: `192.0.0.0 – 223.255.255.255`
- Network Bits: 24
- Host Bits: 8
- Use: Small Networks
- Example: Home and Small Businesses

---

## Class D

- Range: `224.0.0.0 – 239.255.255.255`
- Use: Multicast Communication
- Example: Video Streaming

---

## Class E

- Range: `240.0.0.0 – 255.255.255.255`
- Use: Experimental and Research
- Not used for Public Networking

---

# Types of IP Addresses

1. Public
2. Private
3. Static
4. Dynamic

---

# SOC Perspective

| IP Type | Meaning |
|---------|---------|
| Private | Internal Traffic |
| Public | External Connection |

### Example

```text
Source      : 192.168.1.10
Destination : 45.77.123.66
```

```text
Internal → External Communication
```

---

# MAC Address

## What is a MAC Address?

A MAC address is a **hardware-level unique identifier**.

**Example:**

```text
00:1A:2B:3C:4D:5E
```

---

# MAC Address Structure

- 48-bit address
- Written in hexadecimal

### Parts

```text
First Half → Manufacturer (OUI)
Second Half → Device ID
```

### OUI

OUI = Organizationally Unique Identifier

- First half identifies the manufacturer.

### Device ID

- Second half identifies the device.

---

# MAC Address Example

```text
A8 : A1 : 59 : 9E : A0 : 7B
|-------------| |-------------|
     OUI          NIC Specific
  Manufacturer      Device
```

- First 3 bytes → Organizationally Unique Identifier
- Last 3 bytes → Network Interface Controller specific

---

# ARP

## ARP - Address Resolution Protocol

ARP maps:

```text
IP → MAC
```

### Example

```text
Who has 192.168.1.1?

Tell me your MAC address.
```

ARP is used to find the MAC address associated with a known IP address.

---

# MAC Address vs IP Address

| MAC Address | IP Address |
|-------------|------------|
| Unique identifier assigned to Network Interface Controller (NIC) | Numerical identifier assigned to a device connected to a computer network |
| Stands for Media Access Control Address | Stands for Internet Protocol Address |
| Hardware / physical identifier | Logical / network identifier |
| Helps uniquely identify the device | Helps identify the location of a device on the network |
| Assigned by manufacturer | Assigned by network administrator or ISP |
| Cannot be changed | Can be changed |
| 48 bits | IPv4 = 32 bits, IPv6 = 128 bits |
| Works in Data Link Layer | Works in Network Layer |

---

# Real SOC Scenario

## Observation

Multiple devices are showing the same MAC address.

### Likely Cause

```text
ARP Spoofing
      /
     /
    MITM
```

Possible attack:

```text
ARP Spoofing / Man-in-the-Middle
```

---

# Day 15 - Key Points

```text
IP Address
→ Device identity + network location

IPv4
→ 32-bit
→ 4 octets

Network Part
→ Identifies the network

Host Part
→ Identifies the device

Subnetting
→ Divides network into smaller networks

CIDR /24
→ 24 network bits + 8 host bits
→ 256 total IPs
→ 254 usable IPs

IPv4
→ 32-bit

IPv6
→ 128-bit

MAC
→ 48-bit hardware identifier

ARP
→ IP → MAC

Same MAC on multiple devices
→ Possible ARP Spoofing / MITM
```
