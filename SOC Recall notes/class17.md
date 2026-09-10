
# SOC Analyst L1 – Day 17 
## Router, Switch, VPN, Firewall, IDS/IPS & Proxy

---

# 🚀 1. 30-Second Recall

- Router = Connects Networks • IP Routing • NAT • Routing Table
- Router Logs = Source IP • Destination IP • Traffic Flow
- Router Alerts = Malicious IP • Outbound Traffic • Data Exfiltration

- Switch = LAN Device • Uses MAC
- Switch Alerts = ARP Spoofing • MAC Flooding • Same MAC on Multiple Ports

- VPN = Encrypted Tunnel • Hide IP • Remote Access
- VPN Types = Remote • Site-to-Site • SSL (443)
- VPN Alerts = Impossible Travel • High Data Transfer • Unusual Country • Multiple Locations

- Firewall = Allow/Deny Traffic
- Firewall Types = Network • Host • Stateful
- Firewall Alerts = Port Scan • Blocked Attacks • RDP Brute Force

- IDS = Detect + Alert
- IPS = Detect + Block
- IDS/IPS Alerts = SQLi • Malware • Exploits
- IDS Challenge = False Positives • Alert Fatigue

- Proxy = Middleman
- Proxy Logs = URLs • Downloads • Uploads • User Activity
- Proxy Alerts = Malicious Domains • Data Exfiltration • Unusual Browsing

- VPN vs Proxy = Encryption vs Usually No Encryption
- Forward Proxy = Client
- Reverse Proxy = Server

- Flow = User → Switch → Router → Firewall → Proxy → Internet

- SOC Visibility
  - Router = IP
  - Switch = MAC
  - Firewall = Allow/Deny
  - IDS/IPS = Attack Alerts
  - Proxy = User Behaviour

---

# 📌 2. Must Remember

## 🌐 Router

**Purpose**

- Connects different networks
- Routes packets using IP

**Functions**

- Routing
- NAT (Private → Public IP)
- Routing Table

**SOC Logs**

- Source IP
- Destination IP
- Traffic Flow

**SOC Indicators**

- Malicious IP Communication
- Suspicious Outbound Traffic
- Data Exfiltration

---

## 🖥️ Switch

**Purpose**

- Connects devices inside a LAN
- Uses MAC addresses

**SOC Indicators**

- Internal Lateral Movement
- MAC Anomalies
- Same MAC on Multiple Ports

**Threats**

- ARP Spoofing
- MAC Flooding

---

## 🔒 VPN

**Purpose**

- Encrypted Tunnel
- Hide Real IP
- Secure Remote Access

### Types

- Remote Access VPN
- Site-to-Site VPN
- SSL VPN (**HTTPS/443**)

### SOC Indicators

- Unusual Country Login
- Impossible Travel
- High VPN Data Transfer
- Suspicious Activity After Login

### Common Abuse

- Hide Identity
- Geo Restriction Bypass
- Internal Network Access

---

## 🛡️ Firewall

**Purpose**

- Allow / Deny Traffic

### Types

- Network Firewall
- Host Firewall
- Stateful Firewall

### SOC Indicators

- Blocked Attack Attempts
- Port Scanning
- Suspicious Outbound Traffic

### Example

```text
3389
↓
500 Attempts
↓
Denied
↓
Possible RDP Brute Force
```

---

## 🚨 IDS / IPS

| IDS | IPS |
|------|------|
| Detect | Detect + Block |
| Passive | Inline |
| Alert SOC | Stop Threat |

### Common Alerts

- SQL Injection
- Malware
- Exploit Attempts

### SOC Challenges

- False Positives
- Alert Fatigue

---

## 🌍 Proxy Server

**Purpose**

- Middleman between User & Internet

### Proxy Logs

- URLs
- Downloads
- Uploads
- User Activity

### SOC Indicators

- Malicious Domains
- Data Exfiltration
- Unusual Browsing

---

## 🔄 VPN vs Proxy

| VPN | Proxy |
|------|------|
| Encrypts Traffic | Usually No Encryption |
| OS Level | Application Level |
| Better Security | Faster |

---

## 🔀 Forward vs Reverse Proxy

**Forward Proxy**

- Client Side
- Outbound Requests
- Anonymity
- Content Filtering

**Reverse Proxy**

- Server Side
- Incoming Requests
- Load Balancing
- Caching
- Security

---

## 🌐 Complete Network Flow

```text
User
↓
Switch
↓
Router
↓
Firewall
↓
Proxy
↓
Internet
```

### SOC Visibility

| Device | SOC Sees |
|---------|----------|
| Router | IP Traffic |
| Switch | MAC Activity |
| Firewall | Allowed / Blocked |
| IDS/IPS | Attack Alerts |
| Proxy | User Behaviour |

---
# RAJU RECALL FORMAT
# SOC Analyst L1 – Day 17 (1) | Reply 2
## Router, Switch, VPN, Firewall, IDS/IPS & Proxy

---

# 💼 3. Interview Q&A (Compressed)

### Q1. Router?
**Ans:** Connects different networks, IP routing, NAT, Routing Table.

---

### Q2. Switch?
**Ans:** Connects LAN devices using MAC addresses.

---

### Q3. VPN?
**Ans:** Encrypted tunnel, hides IP, secure remote access.

---

### Q4. VPN Types?
**Ans:** Remote Access • Site-to-Site • SSL VPN (443)

---

### Q5. VPN Abuse Indicators?
**Ans:** Impossible Travel • Unusual Country • Multiple Locations • High Data Transfer.

---

### Q6. Firewall?
**Ans:** Allows/Denies traffic using security rules.

---

### Q7. Firewall Types?
**Ans:** Network • Host • Stateful

---

### Q8. IDS vs IPS?
**Ans:**

- IDS = Detect + Alert
- IPS = Detect + Block

---

### Q9. IDS/IPS Alerts?
**Ans:** SQLi • Malware • Exploit Attempts

---

### Q10. Proxy?
**Ans:** Middleman between user and Internet.

---

### Q11. VPN vs Proxy?
**Ans:** VPN = Encryption • Proxy = Usually no encryption.

---

### Q12. Forward vs Reverse Proxy?
**Ans:**

- Forward = Client side
- Reverse = Server side

---

# 🛡️ 4. SOC Analyst Mindset

```text
Alert
   ↓
Where?

Router
Switch
Firewall
IDS/IPS
Proxy

↓

Collect Logs

↓

Correlate

↓

Attack?

↓

Escalate / Close
```

### Router

- Malicious IP
- Outbound Traffic
- Data Exfiltration

### Switch

- Same MAC
- ARP Spoofing
- MAC Flooding

### VPN

- Impossible Travel
- High VPN Usage
- Suspicious Login

### Firewall

- Port Scan
- Blocked Attack
- RDP Brute Force

### IDS / IPS

- SQLi
- Malware
- Exploit

### Proxy

- Malicious URL
- Unusual Browsing
- Data Exfiltration

---

# 📝 5. Question Paper Mode

1. What is a Router?
2. What are Router functions?
3. What logs does a Router provide?
4. What is a Switch?
5. Which attacks target a Switch?
6. What is a VPN?
7. Name VPN types.
8. What is Impossible Travel?
9. What is a Firewall?
10. Difference between IDS and IPS?
11. What alerts does IDS/IPS generate?
12. What is a Proxy?
13. VPN vs Proxy?
14. Forward vs Reverse Proxy?
15. What logs does a Proxy provide?
16. Explain the complete User → Internet flow.
17. Which device would you investigate for IP, MAC, blocked traffic, attack alerts and user activity?
18. Explain the malware infection scenario.

---

# ✅ 6. Answer Key

**1.** Connects different networks.

**2.** Routing • NAT • Routing Table.

**3.** Source IP • Destination IP • Traffic Flow.

**4.** Connects LAN devices using MAC.

**5.** ARP Spoofing • MAC Flooding.

**6.** Encrypted tunnel.

**7.** Remote Access • Site-to-Site • SSL VPN.

**8.** Same user appears from distant locations in an impossible time.

**9.** Allows/Denies traffic.

**10.**

- IDS = Detect + Alert
- IPS = Detect + Block

**11.** SQLi • Malware • Exploit Attempts.

**12.** Middleman between user and Internet.

**13.**

- VPN = Encryption
- Proxy = Usually no encryption

**14.**

- Forward = Client
- Reverse = Server

**15.**

- URLs
- User Activity
- Downloads
- Uploads

**16.**

```text
User
↓
Switch
↓
Router
↓
Firewall
↓
Proxy
↓
Internet
```

**17.**

- Router → IP Traffic
- Switch → MAC Activity
- Firewall → Allowed/Blocked
- IDS/IPS → Attack Alerts
- Proxy → User Behaviour

**18.**

```text
Firewall → Allowed
Proxy → Suspicious URL
IDS → Malware

↓

Possible Malware Infection
```

---