# Day 18
# DNS Footprinting, DNS Poisoning & APT

---

# 1. 30-Second Recall

## DNS Footprinting
- DNS se target ki information collect karna.
- Reconnaissance stage.
- No direct hacking; information gathering.
- Find:
  - Subdomains
  - Internal services
  - Mail servers
  - Public IPs
  - Infrastructure layout
  - DNS records

## DNS Poisoning
- Fake DNS responses inject karna.
- Domain → Wrong IP
- User ko fake/malicious website par redirect kar sakta hai.
- Goals:
  - Credential theft
  - Malware delivery
  - Phishing

## APT
- Advanced Persistent Threat.
- Targeted + long-term attack.
- Attacker network mein access gain karke hidden rehta hai.
- Goal is usually strategic, not quick gain.

---

# 2. Must Remember

## DNS Footprinting

### Attacker Goal
Maximum information collect karna without detection.

### Important Targets

```text
admin.company.com
dev.company.com
vpn.company.com
mail.company.com
```

Can reveal:
- Subdomains
- Internal naming patterns
- DNS structure
- Infrastructure information

### SOC Indicators

- High number of DNS queries from one IP.
- Sequential subdomain queries.
- External IP querying many domains.

### Example

```text
Source IP: 45.12.x.x

Queries:
admin.company.com
vpn.company.com
mail.company.com
dev.company.com
```

→ Possible DNS Footprinting / Active Reconnaissance

---

# 3. DNS Poisoning

## Basic Flow

```text
Attacker
   ↓
Fake DNS Response
   ↓
DNS Resolver
   ↓
Wrong IP
   ↓
Fake Website
   ↓
Credential Theft / Malware
```

### Real Attack Flow

```text
1. Attacker poisons DNS
2. User types bank.com
3. DNS returns attacker IP
4. Fake login page appears
5. User enters credentials
6. Credentials are stolen
```

---

## Types of DNS Poisoning

### Cache Poisoning
- Malicious DNS data injected into DNS resolver cache.

### Hosts File Poisoning
- Local hosts file modified to redirect domains to malicious IPs.

### Router DNS Poisoning
- Router DNS settings changed to use malicious DNS.

---

## DNS Poisoning Indicators

- Domain resolves to unusual/unrecognized IP.
- Sudden IP change for normally stable domain.
- Certificate warnings.
- Multiple users report different website behavior.
- High number of failed DNS queries.
- Unusual external DNS servers communicating with clients.

### Example

```text
google.com → Unknown IP
```

User:

> "Google looks different."

→ Possible DNS Poisoning

---

# 4. DNS Poisoning Prevention

- Use DNSSEC to validate DNS responses.
- Use secure/trusted DNS resolvers.
- Keep DNS software updated.
- Implement DNS monitoring and alerting.
- Use firewalls/IDS to detect abnormal DNS traffic.
- Monitor users and DNS queries.

---

# 5. DNS Footprinting vs DNS Poisoning

| Feature | Footprinting | Poisoning |
|---|---|---|
| Stage | Recon | Attack |
| Goal | Information Gathering | Redirection |
| Visibility | Low | Medium |
| Impact | Planning | Compromise |

⭐ **Interview Important**

```text
Footprinting = Find information

Poisoning = Manipulate DNS to redirect users
```

---

# 6. SOC Analyst Mindset - DNS

Don't ask only:

> "What domain is this?"

Ask:

```text
Why is this domain being queried?

Is the query pattern normal?

Is the DNS response correct?
```

Always correlate:

```text
Domain
+
Source IP
+
DNS Response
+
Query Frequency
+
Pattern
```

---

# 7. APT - Advanced Persistent Threat

## Definition

APT is a:

- Targeted
- Long-term
- Multi-stage cyber attack

where attackers gain access and remain hidden inside a network for a long time.

---

## Advanced

Uses sophisticated techniques such as:

- Custom malware
- Zero-days
- Evasion techniques

## Persistent

- Remains in the system for weeks/months/years.
- Maintains access even after detection attempts.

## Threat

- Organized attackers.
- Often nation-state or highly skilled groups.

---

# 8. APT Attack Cycle

```text
1. Reconnaissance
        ↓
2. Weaponization
        ↓
3. Delivery
        ↓
4. Initial Access
        ↓
5. Execution
        ↓
6. Persistence
        ↓
7. Privilege Escalation
        ↓
8. Credential Access
        ↓
9. Discovery
        ↓
10. Lateral Movement
        ↓
11. Command & Control (C2)
        ↓
12. Exfiltration & Impact
```

---

# 9. Important APT Indicators

⭐ **Interview Important**

- Low and slow activity.
- Unusual login patterns.
- Internal lateral movement.
- Suspicious PowerShell usage.
- Data exfiltration.
- Unknown domains / C2.
- Unusual outbound connections.
- Multiple systems accessed.
- Large data transfers.
- Persistence mechanisms.

---

# 10. APT Attack Chain Example

```text
Phishing Email
      ↓
PowerShell Executed
      ↓
Mimikatz Dumps Credentials
      ↓
Admin Login
      ↓
RDP to Multiple Servers
      ↓
Data Transfer to External IP
```

### Conclusion

This is not a collection of unrelated alerts.

It indicates an:

**APT-style attack chain**

---

# 11. APT vs Normal Attack

| Feature | Normal Attack | APT |
|---|---|---|
| Duration | Short | Long |
| Goal | Quick Gain | Strategic |
| Detection | Easier | Hard |
| Behavior | Noisy | Stealthy |

---

# 12. SOC Analyst Mindset

Never think:

> "This is just one alert."

Think:

> **"Is this alert part of a bigger attack chain?"**

Example:

```text
Phishing
  ↓
PowerShell
  ↓
Credential Dumping
  ↓
Admin Login
  ↓
Lateral Movement
  ↓
C2
  ↓
Exfiltration
```

Multiple weak indicators can become a **strong attack story when correlated**.

---

# 13. ⭐ Interview Q&A

### Q1. What is DNS Footprinting?
A. Collecting information about a target using DNS during reconnaissance.

### Q2. What can attackers discover through DNS Footprinting?
A. Subdomains, internal services, mail servers, public IPs and infrastructure information.

### Q3. What is DNS Poisoning?
A. Injecting fake DNS responses so a domain resolves to the wrong IP.

### Q4. What is the main goal of DNS Poisoning?
A. Redirect users to malicious sites for credential theft, phishing or malware delivery.

### Q5. Name DNS Poisoning types.
A.
- Cache Poisoning
- Hosts File Poisoning
- Router DNS Poisoning

### Q6. What is an APT?
A. A targeted, long-term cyber attack where attackers maintain hidden access inside a network.

### Q7. What does "Persistent" mean in APT?
A. Attackers maintain access for a long period, potentially weeks, months or years.

### Q8. Name important APT indicators.
A.
- Low and slow activity
- Unusual logins
- Lateral movement
- PowerShell usage
- Data exfiltration
- Unknown C2 domains

### Q9. Why is APT difficult to detect?
A. It is stealthy, long-term and designed to blend with normal activity.

### Q10. What should a SOC Analyst ask when investigating multiple alerts?
A. Whether they are part of a larger attack chain.

---

# 14. Question Paper Mode

1. What is DNS Footprinting?
2. What information can DNS Footprinting reveal?
3. What are the SOC indicators of DNS Footprinting?
4. What is DNS Poisoning?
5. Explain the DNS Poisoning attack flow.
6. What are the types of DNS Poisoning?
7. What are the indicators of DNS Poisoning?
8. How can DNS Poisoning be prevented?
9. Differentiate DNS Footprinting and DNS Poisoning.
10. What questions should a SOC Analyst ask when investigating DNS logs?
11. What is APT?
12. Explain Advanced, Persistent and Threat in APT.
13. Explain the APT attack cycle.
14. What are important SOC indicators of APT?
15. Explain the given APT attack scenario.
16. Differentiate APT from a normal attack.
17. Why should a SOC Analyst correlate multiple alerts?

---

# 15. Answer Key

1. DNS-based information gathering during reconnaissance.
2. Subdomains, services, mail servers, public IPs and infrastructure.
3. High DNS query volume, sequential subdomain queries, unusual external IP querying many domains.
4. Injecting fake DNS responses to redirect domains to wrong IPs.
5. Poison DNS → user requests domain → wrong IP returned → fake site → credentials stolen.
6. Cache, Hosts File, Router DNS Poisoning.
7. DNS mismatch, sudden IP change, certificate warnings, multiple users affected, unusual DNS activity.
8. DNSSEC, trusted resolvers, updates, monitoring, firewall/IDS.
9. Footprinting = reconnaissance/information gathering; Poisoning = attack/redirection.
10. Why is the domain queried? Is the pattern normal? Is the response correct?
11. Targeted, long-term cyber attack where attackers maintain hidden access.
12. Advanced = sophisticated techniques; Persistent = long-term access; Threat = organized/skilled attackers.
13. Recon → Weaponization → Delivery → Initial Access → Execution → Persistence → Privilege Escalation → Credential Access → Discovery → Lateral Movement → C2 → Exfiltration/Impact.
14. Low-and-slow activity, unusual logins, lateral movement, PowerShell, exfiltration, unknown C2 domains.
15. Phishing → PowerShell → credential dumping → admin login → RDP → external data transfer.
16. Normal = short/noisy/quick gain; APT = long/stealthy/strategic.
17. To determine whether individual alerts form part of a larger attack chain.