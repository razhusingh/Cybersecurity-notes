# Day 17 - Networking Devices

---

# Router

## What is a Router?

A Router is a networking device that connects different networks and forwards packets based on IP addresses.

### Functions

- Connects different networks.
- Routes packets using IP addresses.
- Selects the best path for packet delivery.
- Performs Network Address Translation (NAT).
- Maintains a Routing Table.

### Routing Table

A Routing Table stores network routes and helps the router decide where packets should be forwarded.

### NAT (Network Address Translation)

Converts:

```text
Private IP  →  Public IP
```

Allows multiple private devices to communicate with the Internet using a public IP address.

### Router Example

```text
PC (192.168.1.10)
        │
        ▼
     Router
        │
        ▼
Internet (8.8.8.8)
```

### SOC Perspective

Router logs help identify:

- Source IP
- Destination IP
- Incoming traffic
- Outgoing traffic
- Suspicious external connections

---

# Switch

## What is a Switch?

A Switch is a networking device that connects devices within the same Local Area Network (LAN).

Unlike a Hub, a Switch forwards data only to the intended device.

### Functions

- Connects devices inside a LAN.
- Uses MAC Addresses for forwarding.
- Reduces unnecessary network traffic.
- Improves communication efficiency.

### MAC Address Table

A Switch maintains a MAC Address Table.

The table maps:

```text
MAC Address  →  Switch Port
```

This allows frames to be sent only to the correct destination.

### Switch Example

```text
PC1
   \
PC2 --- Switch --- PC3
   /
PC4
```

### SOC Perspective

Switch logs help detect:

- MAC Address changes
- Internal communication
- Suspicious lateral movement
- Duplicate MAC addresses

### Common Threats

#### ARP Spoofing

- Attacker sends fake ARP replies.
- Victim maps the wrong MAC address.
- Can lead to Man-in-the-Middle (MITM) attacks.

#### MAC Flooding

- Attacker floods the switch with fake MAC addresses.
- MAC table becomes full.
- Switch may start broadcasting traffic like a Hub.

---

# VPN (Virtual Private Network)

## What is a VPN?

A VPN creates a secure and encrypted tunnel between a user and a remote network over the Internet.

### Purpose

- Secure communication
- Encrypt network traffic
- Protect sensitive data
- Enable remote access

### VPN Tunnel

```text
User
   │
Encrypted Tunnel
   │
VPN Server
   │
Company Network
```

### Types of VPN

#### 1. Remote Access VPN

- Connects a single user to an organization's network.
- Commonly used for Work From Home (WFH).

#### 2. Site-to-Site VPN

- Connects two different office networks securely.
- Used between branch offices.

#### 3. SSL VPN

- Uses HTTPS (SSL/TLS).
- Allows secure browser-based remote access.

### VPN Benefits

- Encrypts traffic.
- Protects data over public networks.
- Hides internal network communication.
- Enables secure remote connectivity.

### SOC Perspective

Monitor for:

- Unusual VPN logins.
- Login from unexpected countries.
- Multiple failed VPN login attempts.
- Large data transfers through VPN.
- VPN login outside normal working hours.

### Example

```text
User
   │
VPN Login
   │
Company Network
```

If the same user logs in from two distant countries within a short time, it may indicate suspicious activity.

---

# Summary

| Device | Primary Function |
|---------|------------------|
| Router | Connects different networks using IP |
| Switch | Connects devices within a LAN using MAC |
| VPN | Provides secure encrypted remote communication |

---

# Firewall

## What is a Firewall?

A Firewall is a network security device that monitors and filters incoming and outgoing network traffic based on predefined security rules.

### Functions

- Allows legitimate traffic.
- Blocks unauthorized traffic.
- Protects internal networks from external threats.
- Enforces security policies.

### Types of Firewall

#### Packet Filtering Firewall
- Filters traffic based on:
  - Source IP
  - Destination IP
  - Port Number
  - Protocol

#### Stateful Firewall
- Tracks active connections.
- Makes decisions based on connection state.

#### Next-Generation Firewall (NGFW)
- Application awareness.
- Intrusion Prevention (IPS).
- Deep Packet Inspection (DPI).
- Malware detection.

### Firewall Rule Example

```text
Allow : HTTPS (Port 443)

Block : Telnet (Port 23)
```

### Firewall Logs

Firewall logs may contain:

- Source IP
- Destination IP
- Source Port
- Destination Port
- Protocol
- Action (Allow / Deny)
- Timestamp

### SOC Perspective

Monitor for:

- Repeated blocked connections.
- Port scanning.
- Brute-force attempts.
- Unusual outbound traffic.
- Traffic to malicious IP addresses.

---

# IDS (Intrusion Detection System)

## What is IDS?

IDS monitors network traffic and generates alerts when suspicious or malicious activity is detected.

### Functions

- Detect suspicious activity.
- Generate alerts.
- Monitor network traffic.
- Help SOC analysts investigate attacks.

### Detection Methods

#### Signature-Based Detection

- Compares traffic with known attack signatures.
- Fast and accurate for known threats.

#### Anomaly-Based Detection

- Detects abnormal behavior.
- Useful for unknown attacks.

### SOC Perspective

Common IDS alerts:

- SQL Injection
- Malware Communication
- Port Scanning
- Exploit Attempts

---

# IPS (Intrusion Prevention System)

## What is IPS?

IPS detects malicious traffic and automatically blocks or prevents the attack.

### Difference Between IDS and IPS

| IDS | IPS |
|-----|-----|
| Detects attacks | Detects and blocks attacks |
| Generates alerts | Takes preventive action |
| Passive | Active |

### SOC Perspective

IPS can automatically:

- Drop malicious packets.
- Block attacker IP addresses.
- Prevent exploit attempts.
- Stop suspicious connections.

---

# Proxy Server

## What is a Proxy Server?

A Proxy Server acts as an intermediary between a user and the Internet.

### Communication Flow

```text
User
   │
Proxy Server
   │
Internet
```

The destination server sees the Proxy Server instead of the user's device.

### Benefits

- Hides client IP address.
- Content filtering.
- Access control.
- Logging and monitoring.
- Caching.

---

# Types of Proxy

## Forward Proxy

- Located between users and the Internet.
- Represents the client.
- Handles outgoing requests.

### Flow

```text
User
   │
Forward Proxy
   │
Internet
```

---

## Reverse Proxy

- Located in front of servers.
- Represents the server.
- Handles incoming requests.

### Flow

```text
Internet
   │
Reverse Proxy
   │
Web Server
```

### Benefits

- Load Balancing
- Security
- SSL Offloading
- Caching
- Hide backend servers

---

# VPN vs Proxy

| VPN | Proxy |
|-----|-------|
| Encrypts traffic | Usually does not encrypt traffic |
| Protects all network traffic | Usually protects application traffic only |
| Higher security | Mainly used for anonymity/filtering |
| Remote secure access | Content filtering & caching |

---

# Complete Network Flow

```text
User
   │
Switch
   │
Router
   │
Firewall
   │
IDS / IPS
   │
Proxy
   │
Internet
```

---

# SOC Visibility

| Device | Information Available |
|---------|----------------------|
| Router | IP Traffic |
| Switch | MAC Activity |
| Firewall | Allowed / Blocked Connections |
| IDS | Attack Alerts |
| IPS | Prevented Attacks |
| Proxy | User Browsing Activity |

---

# Real SOC Scenario

## Scenario

A user downloads a file from an unknown website.

### Event Flow

```text
User
   │
Firewall
   │
Proxy
   │
IDS
```

### Observations

#### Firewall

```text
Action : Allowed
```

The connection was permitted.

---

#### Proxy

```text
URL : Unknown Domain
```

The user accessed a suspicious website.

---

#### IDS

```text
Alert : Malware Detected
```

Malicious traffic was identified.

---

## SOC Investigation

Check:

- Source User
- Source IP
- Destination URL
- Downloaded File
- File Hash
- IDS Alert
- Firewall Logs
- Proxy Logs

---

## Conclusion

The activity indicates a possible malware download attempt and should be investigated immediately.

---
