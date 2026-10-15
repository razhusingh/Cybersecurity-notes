
# SOC Analyst L1 — Class 33
# Network Security Essentials

## 1. Network Security Essentials

Before defending a network, a SOC analyst must understand:
- What each network asset does.
- What security risks affect that asset.
- Which logs and activities should be monitored.

A network contains different components that work together to enable communication, data access and business operations.

## 2. Main Components of a Network

### 2.1 Endpoints

**What are they?**

Devices employees use to access the network and applications.

**Examples:**
- Desktop computers and laptops.
- Smartphones and tablets.
- Printers.
- IoT devices.

**Security risks:**
- Phishing.
- Malicious downloads.
- Initial access for attackers.

**What should a SOC monitor?**
- EDR alerts.
- Unauthorized script execution.
- Suspicious outbound traffic.

**Easy explanation:** An employee's laptop may be the first device compromised through a phishing email.

### 2.2 File and Database Servers

**What are they?**

Servers that store and manage organizational data and files.

**Examples:**
- File servers using SMB or NAS.
- Database servers such as SQL and NoSQL databases.

**Security risks:**
- Ransomware encrypting files.
- Unauthorized data exfiltration.
- Data theft.

**What should a SOC monitor?**
- File access logs.
- Unusual bulk file reads or writes.
- Unauthorized network connections.

**Easy explanation:** If a server suddenly has thousands of files accessed or modified, the SOC should investigate possible data theft or ransomware activity.

### 2.3 Application Servers

**What are they?**

Servers that host applications and services used across an organization.

**Examples:**
- Web servers using HTTP/HTTPS.
- Email servers using SMTP/IMAP.
- VPN servers.
- Other application servers.

**Security risks:**
- SQL injection.
- Exploitation of unpatched software.
- Brute-force attacks.

**What should a SOC monitor?**
- Application and web logs.
- Web Application Firewall (WAF) alerts.
- Failed authentication attempts.

**Easy explanation:** An exposed web or VPN server can become an entry point if attackers exploit vulnerabilities or guess passwords.

### 2.4 Active Directory and Authentication Servers

**What are they?**

Systems that manage identities, authentication and access control.

**Examples:**
- Active Directory (AD).
- LDAP servers.
- RADIUS/TACACS+.
- Single Sign-On (SSO).

**Security risks:**
- Privilege escalation.
- Kerberoasting.
- Password spraying.
- Lateral movement.

**What should a SOC monitor?**
- Authentication logs.
- Domain Admin logon events.
- Access outside normal working hours.

**Easy explanation:** Active Directory manages user identities and permissions. If an attacker compromises a privileged account, they may gain access to many systems.

### 2.5 Routers and Switches

**What are they?**

Network devices that direct traffic within and between networks.

- **Routers:** Route traffic between different networks.
- **Switches:** Connect devices within the same network, such as a LAN.

**Security risks:**
- Man-in-the-Middle (MitM) attacks.
- Traffic interception.
- Rogue routing paths.

**What should a SOC monitor?**
- Network configuration changes.
- Flow data, including NetFlow/IPFIX.

**Easy explanation:** A compromised network device may redirect traffic or allow an attacker to intercept communications.

### 2.6 Firewalls and Perimeter Devices

**What are they?**

Devices that inspect and filter traffic between trusted and untrusted networks.

**Examples:**
- Next-Generation Firewalls (NGFW).
- IDS/IPS.
- Web Application Firewalls (WAF).
- Gateway/perimeter security devices.

**Security risks:**
- Misconfigured rules.
- Attempts to bypass security controls.
- Distributed Denial-of-Service (DDoS) attacks.

**What should a SOC monitor?**
- Allowed and blocked connection logs.
- Port-scan alerts.
- VPN connection logs.

**Easy explanation:** A firewall decides which network traffic is allowed or blocked. Its logs help analysts identify suspicious connections.

## 3. Asset Monitoring — Quick Comparison

| Asset | Main Role | Important Risks | Monitoring Priorities |
|---|---|---|---|
| Endpoints | Employee work | Phishing, malicious downloads | EDR, unauthorized scripts, outbound traffic |
| File/database servers | Store business data | Ransomware, data theft | File access, bulk reads/writes, connections |
| Application servers | Host web, email and VPN services | SQL injection, exploits, brute force | Web logs, WAF alerts, failed logins |
| AD/identity servers | Manage identities and permissions | Privilege escalation, Kerberoasting, password spraying | Authentication, Domain Admin logons, off-hours access |
| Routers/switches | Direct network traffic | MitM, interception, rogue routes | Configuration changes, NetFlow/IPFIX |
| Firewalls/perimeter devices | Filter network traffic | Misconfiguration, bypass, DDoS | Allow/deny logs, port scans, VPN logs |

**SOC takeaway:** Understand the role of each asset so you know which attacks to look for and which logs to investigate.

---

## 4. Network Visibility: Host-Centric vs Network-Centric Logs

A fundamental security principle is:

**You cannot defend what you cannot see.**

A SOC needs visibility into both what happens on individual systems and what happens as traffic moves across the network.

### 4.1 Host-Centric Logs

**What are they?**

Logs generated directly by operating systems and endpoint security tools.

**Sources:**
- Windows Event Logs: Security, System and Application.
- Linux syslog.
- macOS Unified Logs.
- EDR and antivirus alerts.

**What do they reveal?**
- Process creation, such as `cmd.exe` or PowerShell.
- File modifications.
- Registry changes.
- User login and logout events.

**Easy analogy:** Host logs are like CCTV cameras inside individual rooms. They show what happened inside a particular computer.

### 4.2 Network-Centric Logs

**What are they?**

Logs generated by network appliances and perimeter devices that monitor traffic between systems.

**Sources:**
- Next-Generation Firewalls (NGFW).
- Intrusion Detection/Prevention Systems (IDS/IPS).
- Web proxies.
- NetFlow/IPFIX receivers.
- VPN gateways.

**What do they reveal?**
- Source IP address.
- Destination IP address.
- Source port.
- Destination port.
- Protocol: TCP, UDP or ICMP.
- Connection state.
- Action taken: Allow, Deny or Drop.

**Easy analogy:** Network logs are like cameras at building entrances and corridors. They show who entered or left and which routes they used.

### 4.3 Host Logs vs Network Logs

| Host-Centric Logs | Network-Centric Logs |
|---|---|
| Show activity inside a system | Show network communications |
| Generated by operating systems and endpoint tools | Generated by network and perimeter devices |
| Reveal processes, file changes and logins | Reveal IPs, ports, protocols and connection actions |
| Help identify what happened on a host | Help identify where traffic went and how it was handled |

## 5. Correlating Host and Network Logs

**Correlation means connecting related evidence from different sources to understand one activity.**

A SOC should not investigate host logs and network logs in isolation.

### Example Investigation

A firewall log shows outbound traffic to a suspicious IP address on port `4444`.

The analyst should then:
1. Identify the suspicious connection in the network logs.
2. Check the relevant host's logs.
3. Identify the process or executable that created the connection.
4. Investigate whether that process and its network activity are suspicious.

**Why is this important?**

- Network logs show the connection.
- Host logs help identify the process responsible.
- Together, they provide a clearer picture of the activity.

**Remember:** Network logs answer where traffic went; host logs help answer what generated it.

---

## 6. Key Perimeter Threats and Attack Patterns

A SOC analyst should recognize common attack patterns at the network perimeter.

### 6.1 Reconnaissance and Port Scanning

**What happens?**

An attacker probes a target to discover accessible ports and services.

**Indicator:**

A single external IP probes hundreds of sequential ports on an internal public IP within a short period.

**SOC investigation:**
- Identify the source IP.
- Examine the destination IP and ports.
- Check the frequency and pattern of connection attempts.

### 6.2 Brute Force and Password Spraying

**What happens?**

- **Brute force:** Repeated attempts to guess a password.
- **Password spraying:** Trying a small number of common passwords against multiple accounts.

**Indicator:**

A high volume of `DENY` or `FAILED_LOGIN` logs targeting:
- SSH — Port `22`.
- RDP — Port `3389`.
- VPN endpoints.

**SOC investigation:**
- Identify the targeted service.
- Check failed authentication patterns.
- Examine the source IP and targeted accounts.
- Look for suspicious successful logins associated with the attempts.

### 6.3 Command and Control (C2) Beaconing

**What happens?**

A compromised system periodically communicates with an attacker's server.

**Indicator:**
- Repeated outbound connection attempts at regular intervals.
- Connections using non-standard ports.
- HTTP/HTTPS traffic to suspicious external domains.

**SOC investigation:**
- Identify the destination IP or domain.
- Check connection timing and repetition.
- Correlate network logs with host logs to identify the process responsible.

### 6.4 Exfiltration

**What happens?**

An attacker transfers data from an organization's network to an external destination.

**Indicator:**

Unusually high outbound traffic from an internal database or file server to an unknown external IP address.

**SOC investigation:**
- Identify the internal source system.
- Check the external destination.
- Examine outbound traffic volume.
- Correlate network activity with file access and host logs.

---

## 7. Final SOC Analyst Summary

### Remember These Four Perimeter Patterns

| Attack Pattern | Key Indicator |
|---|---|
| Reconnaissance/port scanning | One external IP probes many ports quickly |
| Brute force/password spraying | High volume of failed or denied login attempts |
| C2 beaconing | Repeated outbound connections, possibly at regular intervals |
| Exfiltration | Unusually high outbound data volume to an unknown external IP |

### The Complete Investigation Mindset

When an alert appears:

1. **Identify the asset:** Endpoint, server, identity system or network device?
2. **Understand the risk:** What attack could affect this asset?
3. **Check the relevant logs:** Host, network, authentication or application logs?
4. **Correlate evidence:** Connect activity across multiple sources.
5. **Investigate the pattern:** Is it scanning, brute force, C2 beaconing or possible exfiltration?
