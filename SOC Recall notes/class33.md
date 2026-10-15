# SOC Analyst L1 — Class 33
# Network Security Essentials

## ⚡ 1. 30-Second Recall

- A network contains endpoints, servers, identity systems, routers, switches and firewalls.
- Every asset has different security risks and monitoring requirements.
- Host-centric logs show activity inside a computer.
- Network-centric logs show communications between systems.
- Correlating both log types helps identify what happened and which process caused the network activity.
- Four important perimeter attack patterns:
  1. Reconnaissance and Port Scanning
  2. Brute Force and Password Spraying
  3. Command and Control (C2) Beaconing
  4. Exfiltration

---

## 🔥 2. MUST REMEMBER

### A. Network Assets

| Asset | Main Risk | What SOC Monitors |
|---|---|---|
| Endpoints | Phishing, malicious downloads | EDR alerts, unauthorized scripts, outbound traffic |
| File/Database Servers | Ransomware, data theft | File access, bulk reads/writes, connections |
| Application Servers | SQL injection, exploits, brute force | Web logs, WAF alerts, failed logins |
| AD/Identity Servers | Privilege escalation, Kerberoasting, password spraying | Authentication logs, Domain Admin logons, off-hours access |
| Routers/Switches | MitM, traffic interception, rogue routing | Configuration changes, NetFlow/IPFIX |
| Firewalls/Perimeter Devices | Misconfigured rules, bypass attempts, DDoS | Allow/deny logs, port scans, VPN logs |

### B. Host-Centric vs Network-Centric Logs

**Host-Centric Logs**
- Sources: Windows Event Logs, Linux syslog, macOS Unified Logs, EDR/antivirus.
- Show: Process creation, file modifications, registry changes, logins/logouts.
- Example: `cmd.exe` or PowerShell execution.

**Network-Centric Logs**
- Sources: NGFW, IDS/IPS, web proxies, NetFlow/IPFIX, VPN gateways.
- Show: Source IP, destination IP, source/destination ports, protocol, connection state and Allow/Deny/Drop action.

**Remember:**
- Host logs = What happened inside the computer?
- Network logs = Where did the traffic go?
- Correlation = Connect both to understand the activity.

### C. Important Investigation Example

**Scenario:** A firewall records outbound traffic to a suspicious IP on port `4444`.

SOC investigation:
1. Identify the suspicious connection in network logs.
2. Identify the affected host.
3. Check host logs to find the process/executable responsible.
4. Investigate whether the process and connection are suspicious.

### D. Four Perimeter Threats

| Threat | Key Indicator | Important Clue |
|---|---|---|
| Reconnaissance/Port Scanning | One external IP probes hundreds of ports quickly | Sequential port probing |
| Brute Force/Password Spraying | High volume of DENY or FAILED_LOGIN events | SSH 22, RDP 3389, VPN |
| C2 Beaconing | Repeated outbound connections, sometimes at regular intervals | Non-standard ports or suspicious external domains |
| Exfiltration | Unusually high outbound traffic to an unknown external IP | Database/file server sending large amounts of data |

### E. Essential Terms

- **EDR:** Endpoint detection and response.
- **WAF:** Web Application Firewall.
- **MitM:** Man-in-the-Middle attack.
- **NetFlow/IPFIX:** Network traffic flow data.
- **C2:** Command and Control communication.
- **Exfiltration:** Transferring data outside the organization.
- **Password spraying:** Trying a small number of common passwords against multiple accounts.
- **Correlation:** Connecting evidence from different log sources.

---

## ⭐ 3. Interview Q&A

**Q1. What is the difference between host-centric and network-centric logs?**

Host logs show activity inside a system. Network logs show communications between systems.

**Q2. Why should a SOC correlate both types of logs?**

To connect network activity with the process or executable responsible for it.

**Q3. What should you investigate if one IP probes hundreds of ports?**

Possible reconnaissance or port scanning. Examine the source IP, destination IP, ports and connection pattern.

**Q4. Which logs can indicate brute-force activity?**

A high volume of failed or denied authentication attempts involving services such as SSH, RDP or VPN.

**Q5. What is C2 beaconing?**

Repeated communication between a compromised system and an attacker's server.

**Q6. What may indicate data exfiltration?**

Unusually high outbound traffic from an internal database or file server to an unknown external IP.

**Q7. What should you check when a firewall reports suspicious outbound traffic?**

Correlate network logs with host logs to identify the process responsible and investigate its behaviour.

**Q8. What should a SOC monitor on Active Directory servers?**

Authentication logs, Domain Admin logon events and access outside normal working hours.

---

## 🧠 4. SOC Analyst Mindset

When an alert appears, ask:

1. **Which asset?** Endpoint, server, identity system or network device?
2. **Which risk?** Phishing, brute force, privilege escalation or data theft?
3. **Which logs?** Host, network, authentication or application?
4. **What connects the evidence?** Correlate related events.
5. **What is the activity?** Scanning, failed logins, C2 beaconing or possible exfiltration?

**Golden rule:** Never depend on one log source when correlating host and network evidence can explain the activity more clearly.

---

## 🗺️ 5. Final Memory Map

**Network Assets**
Endpoints → File/Database Servers → Application Servers → AD/Identity → Routers/Switches → Firewalls

**Visibility**
Host Logs + Network Logs → Correlation → Better Investigation

**Perimeter Threats**
- Scanning → Many ports.
- Brute Force → Many failed logins.
- C2 → Repeated outbound connections.
- Exfiltration → Unusual outbound data volume.

## ✅ Final 30-Second Revision

- Know each asset's role, risk and monitoring priorities.
- Host logs show internal system activity.
- Network logs show traffic and connection details.
- Correlate both to identify the process behind suspicious traffic.
- Recognize port scanning, brute force/password spraying, C2 beaconing and exfiltration.
