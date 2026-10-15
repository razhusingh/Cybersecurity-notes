
# SOC Analyst L1 — Class 30
# Pyramid of Pain & Unified Kill Chain

# 1. Pyramid of Pain

## 1.1 What Is the Pyramid of Pain?

The Pyramid of Pain is a cybersecurity threat intelligence framework introduced by David J. Bianco in 2013.

It explains how much difficulty an attacker faces when a SOC detects and blocks different types of indicators.

**Simple explanation:**

Imagine an attacker keeps changing their malware. Blocking one file hash is easy to bypass. But if the SOC detects the attacker's entire method, the attacker has to work much harder.

- Bottom of the pyramid = less pain for the attacker.
- Top of the pyramid = more pain for the attacker.

The pyramid has six layers.

## 1.2 The Six Layers

### 1. Hash Values — Trivial Pain

**What is a hash?**

A hash is a unique fingerprint of a file.

Examples: MD5, SHA-1 and SHA-256.

**How does a SOC use it?**
- Add a malicious file's hash to an EDR or SIEM detection/blocking system.
- If the same file appears again, the system can identify or block it.

**Why is it easy for attackers to bypass?**

Even changing one byte of a file can change its hash. Attackers can modify malware or use polymorphic code to produce different hashes.

**Remember:** Hashes help detect known files, but modified malware may have a new hash.

### 2. IP Addresses — Negligible Pain

An IP address identifies a network address. Attackers may use IPs for Command and Control (C2) servers or proxies.

Example: `192.0.2.1`

**How does a SOC block it?**
- Firewall rules.
- IP blocklists.

**Why is the pain low?**

Attackers can quickly switch to another IP using botnets, hosting services or cloud instances such as AWS and Azure.

**Remember:** Blocking an IP may interrupt an attack, but the attacker can change infrastructure.

### 3. Domain Names — Slight Pain

A domain name is a human-readable web address that may point to attacker infrastructure.

Example: `malicious-login-update.com`

**How does a SOC block it?**
- DNS sinkholing.
- Web proxy filters.

**Why is the pain slightly higher than blocking an IP?**

Attackers may need to register another domain, configure DNS and wait for propagation.

However, Domain Generation Algorithms (DGAs) can generate many backup domains automatically.

**Remember:** Attackers can replace domains, but doing so requires additional work.

### 4. Network/Host Artifacts — Annoying Pain

Artifacts are traces left by an attacker's tools on a network or computer.

**Network artifacts:**
- Custom HTTP User-Agent strings.
- Unique URI paths.
- Specific TLS certificate hashes.

**Host artifacts:**
- Specific registry keys.
- Distinctive file names.
- Unique mutexes in system memory.

**How does a SOC detect them?**
- NIDS tools such as Snort and Suricata.
- YARA rules.
- Network and endpoint detection rules.

**Why is the attacker's pain higher?**

The attacker may need to modify the tool's code, change its behaviour, recompile it and deploy it again.

**Remember:** Detecting distinctive traces forces attackers to modify their tools, not just replace an indicator.

### 5. Tools — Challenging Pain

Tools are software, utilities or scripts used to conduct attacks.

Examples:
- **Mimikatz:** Credential and password dumping.
- **Cobalt Strike:** C2-related operations.
- **PsExec:** Remote execution and lateral movement.

**How does a SOC detect them?**
- EDR rules.
- Behavioural monitoring.
- AV/EDR signatures.
- Memory scans.

**Why is the pain challenging?**

If the attacker's main tool is detected and blocked, they may need to find, learn or develop a replacement.

**Remember:** Blocking the attacker's tools can disrupt their operations significantly.

### 6. TTPs — Severe Pain

TTPs means **Tactics, Techniques and Procedures**.

They describe how an attacker operates throughout an attack.

Example:
1. Send a spearphishing attachment.
2. Dump LSASS memory to steal credentials.
3. Use PowerShell for malicious execution.

TTPs are represented in the MITRE ATT&CK Framework.

**How does a SOC detect them?**
- Threat hunting.
- Custom detection analytics.
- SIEM correlation.
- EDR behavioural rules.
- Operating-system hardening.

**Why is the pain severe?**

If the SOC blocks an attack technique, the attacker may have to develop or learn a different method. This can require substantial research and effort.

**Remember:** Detecting attacker behaviour is generally more difficult to evade than simply changing a file hash.

## 1.3 Pyramid of Pain — Quick Comparison

| Layer | Example | Detection Method | Attacker's Pain |
|---|---|---|---|
| TTPs | LSASS credential dumping | EDR behaviour rules, MITRE mapping | Severe |
| Tools | Mimikatz, Cobalt Strike | AV/EDR, memory scans | Challenging |
| Network/Host Artifacts | Registry keys, User-Agent | YARA, IDS signatures | Annoying |
| Domain Names | Malicious domain | DNS sinkholing, proxy filters | Slight |
| IP Addresses | Malicious IP | Firewall ACLs, IP reputation | Negligible |
| Hash Values | MD5/SHA-256 | File reputation, blocklists | Trivial |

**Memory trick:** Hash → IP → Domain → Artifacts → Tools → TTPs.

Going upward means increasing pain for the attacker.

## 1.4 How Does a SOC Use the Pyramid?

### Automate the Bottom Three Layers

The SOC can use SIEM and SOAR to consume threat intelligence feeds and automate repetitive actions involving:
- Hash values.
- IP addresses.
- Domain names.

This saves analysts from manually handling every indicator.

### Focus Human Analysts on the Top Layers

Tier 2/Tier 3 analysts and Threat Hunters focus more on:
- Identifying attacker tools.
- Understanding attacker behaviour.
- Mapping activity to TTPs.
- Advanced detection and threat hunting.

**Main lesson:** Automate repetitive indicator-based work and use human expertise to investigate attacker behaviour.

---

# 2. Unified Kill Chain (UKC)

## 2.1 What Is the Unified Kill Chain?

The Unified Kill Chain (UKC) is a cyber threat framework developed by security researcher Paul Pols.

It was designed to address limitations of the traditional Lockheed Martin Cyber Kill Chain and complement MITRE ATT&CK.

UKC contains:
- **18 tactics**
- **3 main phases**

## 2.2 Why Do We Need UKC?

Older security models often described attacks as a simple sequence:

Infect → Execute → Explode

But real attackers may:
- Enter a network.
- Stay hidden for months.
- Move between computers.
- Steal credentials.
- Gain higher privileges.
- Establish backup communication channels.

UKC helps SOC analysts understand the attacker's journey, including activity inside the organization.

## 2.3 The Three Phases

| Phase | Tactics | Simple Meaning |
|---|---|---|
| Infiltration | 1–8 | Get inside and establish control |
| Propagation | 9–14 | Expand access inside the network |
| Action | 15–18 | Achieve the attacker's final objective |

Memory trick:

**Enter → Expand → Achieve**

---

# 3. Phase 1 — Infiltration

The attacker tries to enter the organization and establish control over an initial computer.

## Tactic 1: Reconnaissance

**Meaning:** Collect information about the target.

Examples:
- Gathering employee and domain information.
- Finding open ports.
- OSINT harvesting.
- Shodan queries.
- LinkedIn scraping.

## Tactic 2: Weaponization

**Meaning:** Prepare a malicious payload and combine it with an exploit or lure.

Example: Embedding a malicious macro inside a Word document.

## Tactic 3: Delivery

**Meaning:** Send the payload to the victim.

Examples:
- Phishing emails.
- Drive-by downloads.
- Exposed RDP ports.

## Tactic 4: Social Engineering

**Meaning:** Manipulate a person into performing an action.

Examples:
- Pretexting calls.
- Repeated or urgent MFA prompts designed to manipulate a user.

## Tactic 5: Exploitation

**Meaning:** Exploit a software vulnerability to execute code.

Example: Exploiting a zero-day vulnerability in an unpatched web proxy.

## Tactic 6: Persistence

**Meaning:** Maintain access even after a reboot or password reset.

Examples:
- Registry auto-run keys.
- Scheduled tasks.

## Tactic 7: Defense Evasion

**Meaning:** Avoid or bypass security controls.

Examples:
- Obfuscating PowerShell scripts.
- Unhooking EDR DLLs.
- Attempting to bypass antivirus, EDR or firewalls.

## Tactic 8: Command and Control (C2)

**Meaning:** Establish communication between a compromised computer and the attacker's server.

Examples:
- HTTPS beaconing.
- DNS tunnelling to a malicious external IP.

### Infiltration Revision

Reconnaissance → Weaponization → Delivery → Social Engineering → Exploitation → Persistence → Defense Evasion → C2

**Goal:** Gain a foothold and establish control over an initial host.

---

# 4. Phase 2 — Propagation

The attacker is already inside and wants to expand access.

The first compromised computer is often called **Patient Zero**.

## Tactic 9: Pivot

**Meaning:** Use the initial compromised computer to reach hidden internal network areas.

Example: Tunnelling SSH traffic through an internal web server.

## Tactic 10: Discovery

**Meaning:** Explore the internal network, Active Directory and available systems.

Examples:
- Running `net group "Domain Admins"`.
- Running BloodHound scans.

## Tactic 11: Privilege Escalation

**Meaning:** Gain higher administrative privileges.

Example: Dumping LSASS memory to obtain administrator credentials or Kerberos-related material using Mimikatz.

## Tactic 12: Execution

**Meaning:** Run malicious code on additional internal computers.

Examples:
- PsExec.
- WMI commands.

## Tactic 13: Credential Access

**Meaning:** Steal credentials or password hashes.

Examples:
- Keylogging.
- Kerberoasting.
- Searching for plaintext credentials in configuration files.

## Tactic 14: Lateral Movement

**Meaning:** Move from one computer to another across the network.

Example: Using stolen Domain Admin tokens to connect to server farms through RDP.

### Propagation Revision

Pivot → Discovery → Privilege Escalation → Execution → Credential Access → Lateral Movement

**Goal:** Expand access, gain privileges, steal credentials and reach more systems.

---

# 5. Phase 3 — Action

The attacker has reached target systems, such as databases, domain controllers or cloud storage, and tries to achieve the final objective.

## Tactic 15: Collection

**Meaning:** Gather targeted files and sensitive information into one location.

Example: Collecting customer database files into ZIP archives on a disk.

## Tactic 16: Exfiltration

**Meaning:** Transfer stolen data outside the organization.

Examples:
- Uploading encrypted ZIP files to Mega.nz.
- Sending data through HTTP POST requests.

## Tactic 17: Impact

**Meaning:** Disrupt, corrupt or destroy business operations.

Examples:
- Ransomware encrypting disks.
- Wiping backups.

## Tactic 18: Objectives

**Meaning:** Achieve the attacker's ultimate goal.

Examples:
- Financial extortion.
- State espionage.
- Reputation destruction.

### Action Revision

Collection → Exfiltration → Impact → Objectives

**Goal:** Gather data, steal it, cause disruption or fulfil the attacker's purpose.

---

# 6. How a Senior SOC Analyst Uses UKC

## 6.1 Alert Mapping

A SOC analyst maps SIEM alerts to the relevant UKC phase.

Examples:
- Phishing link clicked → Phase 1: Infiltration.
- LSASS memory read → Phase 2: Propagation.

This connects individual alerts into a bigger attack story.

## 6.2 Determine Incident Scope

The phase reached helps the SOC understand how far the attack has progressed.

- **Phase 1:** The incident may still be contained.
- **Phase 2 or 3:** It may indicate an active enterprise breach.

Possible responses include:
- Isolating affected hosts.
- Resetting Active Directory passwords.
- Escalating the incident to executives.

## 6.3 Break the Attack Chain

The SOC does not need to block every tactic. It needs to interrupt a critical part of the attack before the attacker reaches the final objective.

**Example:**

If the SOC blocks lateral movement in Phase 2, the attacker may be prevented from reaching the systems needed to steal data during Phase 3.

### SOC Analyst Mindset

When investigating an incident, ask:
- Which phase has the attacker reached?
- What has the attacker done already?
- Which systems or identities are affected?
- What might happen next?
- Where can we interrupt the attack?

---

# 7. Compare the Three Frameworks

| Framework | Scope | Focus | Main Advantage |
|---|---|---|---|
| Lockheed Martin Cyber Kill Chain | 7 high-level steps | Perimeter defense and prevention | Easy for management to understand |
| MITRE ATT&CK | Hundreds of techniques | Specific attacker behaviours | Useful for tactical EDR/SIEM detection |
| Unified Kill Chain | 18 tactics, 3 phases | Full attack lifecycle | Combines detailed behaviours with an attack timeline |

## Lockheed Martin Cyber Kill Chain

- Uses seven high-level steps.
- Focuses on perimeter defense and prevention.
- Easy to understand.
- Has limitations when representing internal breaches.

## MITRE ATT&CK

- Contains hundreds of techniques.
- Describes specific attacker behaviours.
- Helps build and map EDR/SIEM detection rules.
- Provides detailed techniques but not the same chronological narrative as UKC.

## Unified Kill Chain

- Contains 18 tactics across three phases.
- Represents the complete attack lifecycle.
- Combines MITRE ATT&CK's tactical detail with a strategic timeline.

---

# 8. Final Revision Map

## Pyramid of Pain

| Bottom to Top | Remember |
|---|---|
| 1. Hash Values | File fingerprint; easy to change |
| 2. IP Addresses | Network address; easy to replace |
| 3. Domain Names | Web address; replacement requires setup |
| 4. Network/Host Artifacts | Traces left by tools |
| 5. Tools | Software used to attack |
| 6. TTPs | Attacker's methods and behaviour |

**Rule:** Higher in the pyramid = greater pain for the attacker.

## Unified Kill Chain — All 18 Tactics

**Phase 1: Infiltration**
1. Reconnaissance
2. Weaponization
3. Delivery
4. Social Engineering
5. Exploitation
6. Persistence
7. Defense Evasion
8. Command and Control

**Phase 2: Propagation**
9. Pivot
10. Discovery
11. Privilege Escalation
12. Execution
13. Credential Access
14. Lateral Movement

**Phase 3: Action**
15. Collection
16. Exfiltration
17. Impact
18. Objectives

**Final memory trick:** Enter → Expand → Achieve.
