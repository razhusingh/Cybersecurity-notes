
# SOC Analyst L1 – Day 15 (2) 
## IP Addressing + MAC Address

---

# 🚀 1. 30-Second Recall

- IP Address = Device Identity + Network Location
- IPv4 = 32-bit, 4 Octets (0–255)
- IPv6 = 128-bit, Hexadecimal
- Network Part = Identifies Network
- Host Part = Identifies Device
- Subnetting = Divide Network into Smaller Networks
- CIDR = Classless Inter-Domain Routing
- /24 = 24 Network Bits + 8 Host Bits
- /24 = 256 Total IPs, 254 Usable
- Network Address = First IP
- Broadcast Address = Last IP
- Common Subnets = /24, /16, /8
- IP Classes = A, B, C, D, E
- IP Types = Public, Private, Static, Dynamic
- Private IP = Internal Traffic
- Public IP = External Communication
- MAC Address = Hardware Identifier
- MAC = 48-bit (Hex)
- OUI = Manufacturer
- Device ID = NIC Identifier
- ARP = IP → MAC Mapping
- Same MAC on Multiple Devices = ARP Spoofing / MITM

---

# 📌 2. Must Remember

## 🌐 IP Address

**IP Address = Unique identifier of a device on a network.**

- Device Identity + Network Location
- Example: **192.168.1.10**
- IPv4 = **32-bit (4 Octets)**

---

## 🏠 Network Part vs Host Part

### Network Part

- Identifies the **network**
- Devices with the same network part belong to the same network

Example:

```text
192.168.1.10

Network = 192.168.1
Host = 10
```

### Host Part

- Identifies the **specific device** inside the network.

---

## 🌐 Subnetting

**Subnetting = Dividing one network into smaller networks.**

### Benefits

- Better Security
- Better Performance
- Easier Management

---

## 📍 CIDR

**CIDR = Classless Inter-Domain Routing**

Example:

```text
192.168.1.0/24
```

Meaning:

- **24 bits = Network**
- **8 bits = Host**

---

## 📊 /24 Subnet

- Total IPs = **256**
- Usable IPs = **254**
- First IP = **Network Address**
- Last IP = **Broadcast Address**

---

## 📑 Common CIDR

| CIDR | Subnet Mask | Usable Hosts |
|------|-------------|-------------:|
| /24 | 255.255.255.0 | 254 |
| /16 | 255.255.0.0 | 65,534 |
| /8 | 255.0.0.0 | ~16 Million |

---

## 🌍 IPv4 vs IPv6

| IPv4 | IPv6 |
|------|------|
| 32-bit | 128-bit |
| Decimal | Hexadecimal |
| Address Exhaustion | Solves Address Shortage |
| IPSec Optional | IPSec Supported |

---

## 🏢 IP Classes

| Class | Range | Use |
|------|------|------|
| A | 1–126 | Large Networks |
| B | 128–191 | Medium Networks |
| C | 192–223 | Small Networks |
| D | 224–239 | Multicast |
| E | 240–255 | Experimental |

> **127.x.x.x = Loopback**

---

## 🌍 Types of IP Address

- Public
- Private
- Static
- Dynamic

### SOC Perspective

- **Private IP → Internal Traffic**
- **Public IP → External Communication**

---

# 💻 MAC Address

**MAC Address = Hardware-level unique identifier**

Example:

```text
00:1A:2B:3C:4D:5E
```

### Structure

- **48-bit**
- Written in **Hexadecimal**

### Parts

- **OUI** → Manufacturer
- **Device ID** → Network Interface Identifier

---

## 🔄 ARP

**ARP = Address Resolution Protocol**

Maps:

```text
IP Address
      ↓
MAC Address
```

Example:

```text
Who has 192.168.1.1?

↓

Tell me your MAC Address
```

---

## 🆚 MAC vs IP

| MAC | IP |
|------|------|
| Hardware Address | Logical Address |
| 48-bit | IPv4 = 32-bit / IPv6 = 128-bit |
| Data Link Layer | Network Layer |
| Normally Fixed | Can Change |

---

## 🛡️ SOC Indicators

### Public IP

→ Internet Communication

### Private IP

→ Internal Communication

### Same MAC Address on Multiple Devices

→ Possible **ARP Spoofing / MITM**

---
# RAJU RECALL FORMAT
# SOC Analyst L1 – Day 15 (2) | Reply 2
## IP Addressing + MAC Address

---

# 🛡️ 3. SOC Analyst Mindset

## IP Address Investigation Workflow

```text
Network Alert
      ↓
Identify Source IP & Destination IP
      ↓
Private or Public?
      ↓
Check Internal or External Communication
      ↓
Identify Network & Host
      ↓
Check Logs (Firewall / SIEM / EDR)
      ↓
Is Activity Normal?
      ↓
Escalate or Close
```

### During Investigation Ask Yourself

- Is the source IP Private or Public?
- Is the destination internal or external?
- Which host is communicating?
- Is the communication expected?
- Is this suspicious outbound traffic?
- Is subnet communication normal?
- Should this alert be escalated?

---

## MAC Address Investigation Workflow

```text
MAC Alert
      ↓
Identify MAC Address
      ↓
Check Vendor (OUI)
      ↓
Check ARP Entries
      ↓
Multiple Devices Using Same MAC?
      ↓
Possible ARP Spoofing / MITM
      ↓
Investigate Further
      ↓
Escalate or Close
```

### During Investigation Ask Yourself

- Which MAC address generated the alert?
- Does the OUI match the expected vendor?
- Are multiple devices using the same MAC?
- Has the ARP table changed unexpectedly?
- Could this indicate ARP Spoofing or MITM?

---

# 💼 4. Interview Q&A

### Q1. What is an IP Address?

**Answer:** A unique logical identifier that identifies a device and its location on a network.

---

### Q2. What is IPv4?

**Answer:** A 32-bit IP address written in decimal format using four octets.

---

### Q3. What is IPv6?

**Answer:** A 128-bit IP address written in hexadecimal to overcome IPv4 address exhaustion.

---

### Q4. Difference between Network Part and Host Part?

**Answer:**

- Network Part → Identifies the network
- Host Part → Identifies the specific device

---

### Q5. What is Subnetting?

**Answer:** Dividing one large network into smaller networks for better security, performance and management.

---

### Q6. What is CIDR?

**Answer:** Classless Inter-Domain Routing, a method for flexible IP addressing and subnetting.

---

### Q7. How many usable IPs are available in a /24 subnet?

**Answer:** 254 usable IP addresses.

---

### Q8. Difference between IPv4 and IPv6?

**Answer:**

- IPv4 = 32-bit
- IPv6 = 128-bit

---

### Q9. What is a MAC Address?

**Answer:** A unique hardware identifier assigned to a network interface.

---

### Q10. What is ARP?

**Answer:** Address Resolution Protocol maps an IP address to a MAC address.

---

### Q11. Difference between MAC Address and IP Address?

**Answer:**

- MAC = Hardware Address
- IP = Logical Address

---

### Q12. Why would multiple devices showing the same MAC address be suspicious?

**Answer:** It may indicate ARP Spoofing or a Man-in-the-Middle (MITM) attack.

---

# 📝 5. Question Paper Mode

1. What is an IP Address?
2. What is IPv4?
3. What is IPv6?
4. Difference between Network Part and Host Part?
5. What is Subnetting?
6. What is CIDR?
7. Explain the meaning of /24.
8. How many total and usable IPs are available in a /24 subnet?
9. Name the common subnet sizes.
10. Differentiate IPv4 and IPv6.
11. Explain IP Address Classes A–E.
12. Name the four types of IP addresses.
13. Difference between Public and Private IP?
14. What is a MAC Address?
15. Explain the structure of a MAC Address.
16. What is OUI?
17. What is ARP?
18. Difference between MAC Address and IP Address?
19. Why is ARP important?
20. What SOC alert could indicate ARP Spoofing?

---

# ✅ 6. Answer Key

**1.** Unique logical identifier of a device on a network.

**2.** 32-bit IP address written in decimal format.

**3.** 128-bit IP address written in hexadecimal.

**4.**

- Network Part → Network
- Host Part → Device

**5.** Dividing a network into smaller subnetworks.

**6.** Classless Inter-Domain Routing.

**7.** /24 = 24 Network Bits + 8 Host Bits.

**8.**

- Total = 256
- Usable = 254

**9.**

- /24
- /16
- /8

**10.**

- IPv4 = 32-bit
- IPv6 = 128-bit

**11.**

- Class A → Large Networks
- Class B → Medium Networks
- Class C → Small Networks
- Class D → Multicast
- Class E → Experimental

**12.**

- Public
- Private
- Static
- Dynamic

**13.**

- Public → External Communication
- Private → Internal Communication

**14.** Hardware-level unique identifier.

**15.** 48-bit hexadecimal address.

**16.** Organizationally Unique Identifier (Manufacturer ID).

**17.** Address Resolution Protocol maps IP addresses to MAC addresses.

**18.**

- MAC = Hardware Address
- IP = Logical Address

**19.** It allows devices to discover the MAC address corresponding to an IP address for communication on a local network.

**20.** Multiple devices showing the same MAC address may indicate ARP Spoofing / MITM.

---

