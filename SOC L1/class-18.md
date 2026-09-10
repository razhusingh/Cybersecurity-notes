# Day 18 - DNS Footprinting, DNS Poisoning & APT

---

# DNS Footprinting

## What is DNS Footprinting?

DNS Footprinting is the process of collecting information about a target using DNS.

- It is part of reconnaissance.
- No hacking yet; mainly information gathering.
- Attacker's goal: Collect maximum information without getting detected.

## What Attackers Try to Find

- Subdomains
  - `admin.company.com`
  - `dev.company.com`
  - `vpn.company.com`
- Internal services
- Mail servers
- Public IP addresses
- Infrastructure layout
- DNS records

---

# DNS Footprinting - SOC Indicators

If DNS logs show queries such as:

```text
admin.site.com
dev.site.com
vpn.site.com
test.site.com
```

This can indicate reconnaissance/footprinting.

Successful enumeration may reveal:

- Subdomains
- Full DNS structure
- Internal naming patterns
- Infrastructure information

## Key Detection Indicators

- High number of DNS queries from one IP.
- Sequential subdomain queries.
- Unusual external IP querying many domains.

## Example

```text
Source IP: 45.12.x.x

Queries:
admin.company.com
vpn.company.com
mail.company.com
dev.company.com
```

### Conclusion

```text
Active Reconnaissance
        ↓
DNS Footprinting
```

---

# DNS Poisoning

## What is DNS Poisoning?

DNS Poisoning means injecting fake DNS responses.

The result is:

```text
Domain → Wrong IP
```

### Goals

- Redirect user to a fake website.
- Steal credentials.
- Deliver malware.

---

# DNS Poisoning - Attack Flow

## Normal DNS Resolution

```text
User
  ↓
DNS Resolver
  ↓
Root Server
  ↓
TLD Server
  ↓
Authoritative DNS Server
  ↓
Correct IP
  ↓
Legitimate Website
```

## DNS Poisoning

```text
Attacker
   ↓
Fake DNS Response
   ↓
DNS Resolver
   ↓
Malicious IP
   ↓
Fake Website
```

If a malicious response is accepted and cached, future users can receive the fake IP.

---

# DNS Cache Poisoning

### Technical Flow

```text
1. Attacker sends DNS query/traffic to the resolver.
2. Resolver forwards the query.
3. Before the legitimate response arrives, attacker sends a fake response.
4. If the fake response matches the expected details, it may be accepted and stored in cache.
5. Future queries use the poisoned cache and return the fake IP.
```

---

# DNS Poisoning Example

```text
1. User wants to visit:
   www.bank.com

2. Attacker poisons DNS resolver.

3. www.bank.com resolves to:
   6.6.6.6

4. User is redirected to a fake bank website.

5. User enters credentials.

6. Attacker steals the credentials.
```

---

# Types of DNS Poisoning

## 1. Cache Poisoning

- Malicious DNS data is injected into the DNS resolver cache.
- Can affect multiple users using the same resolver.

## 2. Hosts File Poisoning

- Local hosts file is modified.
- Domains are redirected to malicious IP addresses.

## 3. Router DNS Poisoning

- DNS settings on the router are changed.
- Devices using that router may receive malicious DNS information.

---

# DNS Poisoning - Indicators

SOC indicators include:

- A domain resolves to an unusual or unrecognized IP address.
- Sudden change in IP for a domain that normally has a static IP.
- Multiple users report certificate warnings.
- Multiple users report that the website looks different.
- High number of failed DNS queries to the same domain.
- Unusual external DNS servers communicating with clients.

---

# DNS Poisoning - Impact

Possible impact:

- Credential theft / phishing
- Malware download
- Financial loss
- Loss of trust and reputation

---

# DNS Poisoning - Prevention & Defense

- Enable DNSSEC to validate DNS responses.
- Use secure and trusted DNS resolvers.
- Regularly update DNS software.
- Implement network monitoring and alerting.
- Use firewalls/IDS to detect abnormal DNS traffic.
- Educate users and secure their computers.

---

# DNS Poisoning - SOC Quick Check

When investigating DNS activity, verify:

1. Domain → IP mapping
2. Source of DNS response
3. Frequency and pattern of DNS queries
4. Compare with Threat Intelligence
   - Malicious IP
   - Malicious domain

---

# Real DNS Poisoning Attack Flow

```text
Attacker poisons DNS
        ↓
User types bank.com
        ↓
DNS returns attacker IP
        ↓
Fake login page shown
        ↓
User enters credentials
        ↓
Credentials stolen
```

## SOC Indicators

- DNS resolution mismatch
- Sudden DNS change
- Certificate warnings
- Multiple users affected

---

# Real SOC Scenario

### User Complaint

```text
"Google looks different"
```

### DNS Log

```text
google.com → Unknown IP
```

### Conclusion

```text
Possible DNS Poisoning Attack
```

---

# DNS Footprinting vs DNS Poisoning

| Feature | Footprinting | Poisoning |
|---------|--------------|-----------|
| Stage | Recon | Attack |
| Goal | Information Gathering | Redirection |
| Visibility | Low | Medium |
| Impact | Planning | Compromise |

---

# SOC Analyst Mindset - DNS

When you see DNS logs, don't only ask:

```text
"What domain is this?"
```

Also ask:

```text
Why is this domain being queried?

Is the pattern normal?

Is the response correct?
```

---

# APT - Advanced Persistent Threat

## What is APT?

APT (Advanced Persistent Threat) is a targeted, long-term cyber attack where attackers gain access and stay hidden inside a network for a long time.

### Advanced

Uses sophisticated techniques such as:

- Custom malware
- Zero-days
- Evasion

### Persistent

- Stays in the system for weeks/months/years.
- Maintains access even after detection attempts.

### Threat

- Organized attackers.
- Often nation-state or skilled groups.

---

# APT Attack Cycle

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

# 1. Reconnaissance

Attacker researches the target and gathers information.

Examples:

- DNS Enumeration
- WHOIS Lookup
- Social Engineering
- Public Data
- LinkedIn

---

# 2. Weaponization

Attacker creates a malicious payload/tool.

Examples:

- Exploit Code
- Malicious Documents
- Backdoor / RAT
- Custom Malware

---

# 3. Delivery

Malicious payload is delivered to the victim.

Examples:

- Phishing Email
- Malicious Link
- USB / Removable Device
- Drive-by Download

---

# 4. Initial Access

Attacker gains a foothold in the target environment.

Examples:

- Exploiting vulnerability
- Malicious macros
- Valid credentials
- Phishing attachment

---

# 5. Execution

Malicious code runs on the compromised system.

Examples:

- PowerShell
- CMD / Bash
- WMI
- LOLBins

---

# 6. Persistence

Attacker establishes a way to maintain access even after reboots.

Examples:

- Registry Run Keys
- Scheduled Tasks
- Services
- WMI Event Subscription

---

# 7. Privilege Escalation

Attacker increases privileges to gain higher access.

Examples:

- Exploit local vulnerability
- Token impersonation
- Credential dumping
- Misconfigurations

---

# 8. Credential Access

Attacker steals or harvests credentials.

Examples:

- Mimikatz
- LSASS Dump
- Password hashes
- Keylogging

---

# 9. Discovery

Attacker explores the network and systems to find useful information.

Examples:

- Network scanning
- Network/IP commands
- Enumerating users
- Share enumeration

---

# 10. Lateral Movement

Attacker moves from one compromised system to another.

Examples:

- RDP / SMB
- PsExec / WMI
- Pass-the-Hash
- Remote Services

---

# 11. Command & Control (C2)

Compromised systems communicate with the attacker's C2 server for commands.

Examples:

- HTTPS / SSL
- DNS Tunnelling
- Custom Protocol
- Beaconing

---

# 12. Exfiltration & Impact

Attacker steals or destroys data.

Examples:

- Data exfiltration
- Compression
- Staging data
- Ransomware / Wiper

---

# APT Attacker Goals

- Steal sensitive data
- Espionage / Intelligence
- Financial gain
- Disruption / Sabotage

---

# APT - Common SOC Indicators

- Unusual outbound connections
- Unknown domains / IPs
- Multiple systems accessed
- PowerShell / WMI abuse
- Credential dumping activities
- Lateral movement patterns
- Unusual login times
- Large data transfers
- Disabled security tools
- Persistence mechanisms

---

# APT - Defense Best Practices

- Keep systems & software updated.
- Use strong email filtering.
- Monitor logs & network traffic.
- Implement EDR / XDR solutions.
- Enforce least privilege access.
- Segment the network.
- Provide regular security awareness training.
- Maintain an incident response plan.

---

# Real SOC Scenario - APT

```text
User opens phishing email
        ↓
PowerShell executed
        ↓
Mimikatz dumps credentials
        ↓
Admin login detected
        ↓
RDP to multiple servers
        ↓
Data transfer to external IP
```

### Conclusion

This is not random activity.

It represents an:

```text
APT-style Attack Chain
```

---

# APT vs Normal Attack

| Feature | Normal Attack | APT |
|---------|---------------|-----|
| Duration | Short | Long |
| Goal | Quick Gain | Strategic |
| Detection | Easier | Hard |
| Behavior | Noisy | Stealthy |

---

# SOC Analyst Mindset - APT

Don't think:

```text
"This is one alert."
```

Think:

```text
"Is this part of a bigger attack chain?"
```

A SOC Analyst should correlate multiple alerts and activities to identify the complete attack chain.

---

# Day 18 - Key Takeaways

```text
DNS Footprinting
→ Recon / Information Gathering

DNS Poisoning
→ Fake DNS Response / Redirection

APT
→ Targeted + Long-term + Stealthy Attack

SOC Approach
→ Correlate individual alerts into the bigger attack chain
```

---
