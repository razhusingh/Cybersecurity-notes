# Pyramid of Pain & Unified Kill Chain

## 1. ⚡ 30-Second Recall

- Pyramid of Pain = Shows how much pain blocking different indicators causes attackers.
- Six layers: Hash → IP → Domain → Network/Host Artifacts → Tools → TTPs.
- Higher pyramid layer = Greater attacker pain.
- UKC = Unified Kill Chain, a framework for understanding the complete cyberattack lifecycle.
- UKC has 18 tactics grouped into 3 phases:
  1. Infiltration — Gain initial access.
  2. Propagation — Expand access internally.
  3. Action — Achieve the final objective.

Memory trick: **Enter → Expand → Achieve**

---

## 2. 🔥 MUST REMEMBER

### A. Pyramid of Pain

| Layer | Key Point | Attacker Pain |
|---|---|---|
| Hash Values | File fingerprint; changes when file changes | Trivial |
| IP Addresses | Can be replaced quickly | Negligible |
| Domain Names | Replacement requires registration and DNS setup | Slight |
| Network/Host Artifacts | Unique traces left by attacker tools | Annoying |
| Tools | Software used to conduct attacks | Challenging |
| TTPs | Attacker's tactics, techniques and procedures | Severe |

### Important Examples

- Hash: MD5, SHA-1, SHA-256.
- IP blocking: Firewall rules and IP blocklists.
- Domain blocking: DNS sinkholing and web proxy filters.
- Network artifacts: HTTP User-Agent, URI paths, TLS certificate hashes.
- Host artifacts: Registry keys, distinctive file names, mutexes.
- Tools: Mimikatz, Cobalt Strike, PsExec.
- TTPs: Spearphishing, LSASS credential dumping, PowerShell execution.

### SOC Use of Pyramid of Pain

- Automate the bottom three layers using SIEM/SOAR and threat intelligence feeds.
- Human analysts and Threat Hunters focus more on tools, behaviours and TTPs.
- Goal: Make attacks more difficult and expensive for attackers.

### B. Unified Kill Chain (UKC)

- Developed by Paul Pols.
- Contains 18 tactics across 3 phases.
- Models modern attacks, including internal movement and prolonged hidden activity.

#### Phase 1 — Infiltration (1–8)

| No. | Tactic | Remember |
|---|---|---|
| 1 | Reconnaissance | Gather target information |
| 2 | Weaponization | Prepare malicious payload |
| 3 | Delivery | Send payload to victim |
| 4 | Social Engineering | Manipulate people |
| 5 | Exploitation | Exploit vulnerability |
| 6 | Persistence | Maintain access |
| 7 | Defense Evasion | Bypass security controls |
| 8 | Command & Control | Communicate with attacker server |

#### Phase 2 — Propagation (9–14)

| No. | Tactic | Remember |
|---|---|---|
| 9 | Pivot | Use compromised host to reach other network areas |
| 10 | Discovery | Explore network and assets |
| 11 | Privilege Escalation | Gain higher privileges |
| 12 | Execution | Run malicious code on additional systems |
| 13 | Credential Access | Steal credentials or hashes |
| 14 | Lateral Movement | Move between computers |

#### Phase 3 — Action (15–18)

| No. | Tactic | Remember |
|---|---|---|
| 15 | Collection | Gather targeted data |
| 16 | Exfiltration | Transfer data outside the organization |
| 17 | Impact | Disrupt or damage operations |
| 18 | Objectives | Achieve the attacker's final goal |

### C. Senior SOC Analyst Uses UKC

- Alert Mapping: Connect SIEM alerts to UKC phases.
- Scope Assessment: Determine how far the attack has progressed.
- Breaking the Chain: Interrupt a critical tactic before the attacker reaches the final objective.

Examples:
- Phishing link clicked → Infiltration.
- LSASS memory read → Propagation.
- Blocking lateral movement may prevent later data exfiltration.

### D. Framework Comparison

| Framework | Main Focus |
|---|---|
| Lockheed Martin Cyber Kill Chain | 7 high-level steps; perimeter defense and prevention |
| MITRE ATT&CK | Detailed attacker behaviours and techniques |
| Unified Kill Chain | 18 tactics across 3 phases; full attack lifecycle |

---

## 3. ⭐ Interview Q&A

**Q1. What is the Pyramid of Pain?**

A. A threat intelligence framework showing how much difficulty blocking different indicators causes attackers.

**Q2. What are the six layers?**

A. Hash Values, IP Addresses, Domain Names, Network/Host Artifacts, Tools and TTPs.

**Q3. Which layer causes the greatest attacker pain?**

A. TTPs, because blocking established techniques may force attackers to develop different methods.

**Q4. What does TTP stand for?**

A. Tactics, Techniques and Procedures.

**Q5. What is the Unified Kill Chain?**

A. A framework representing the full cyberattack lifecycle using 18 tactics across 3 phases.

**Q6. Name the three UKC phases.**

A. Infiltration, Propagation and Action.

**Q7. What is the difference between privilege escalation and lateral movement?**

A. Privilege escalation gains higher privileges; lateral movement moves between systems.

**Q8. What is exfiltration?**

A. Transferring collected data outside the organization.

**Q9. How does a SOC use UKC?**

A. To map alerts, assess attack progression and identify where to interrupt the attack.

**Q10. How do MITRE ATT&CK and UKC differ?**

A. MITRE ATT&CK provides detailed attacker techniques; UKC organizes the attack lifecycle into a chronological framework.

---

## 4. 🧠 SOC Analyst Mindset

When investigating an alert, ask:

1. What did the attacker do?
2. Which UKC phase does the activity belong to?
3. Which systems and accounts are affected?
4. Is the attacker escalating privileges or moving laterally?
5. Can the attack be stopped before data exfiltration or impact?

**Remember:** Don't investigate alerts in isolation. Connect the evidence to understand the attacker's journey.

---

## 5. 📝 Question Paper Mode

### MCQs

**Q1. Which Pyramid of Pain layer causes the greatest attacker pain?**

A. Hash Values  
B. IP Addresses  
C. Tools  
D. TTPs

**Q2. Which mechanism can block malicious domains?**

A. DNS sinkholing  
B. Disk formatting  
C. Password rotation only  
D. File compression

**Q3. How many tactics are in the Unified Kill Chain?**

A. 7  
B. 10  
C. 18  
D. 20

**Q4. Lateral Movement belongs to which UKC phase?**

A. Infiltration  
B. Propagation  
C. Action  
D. Reconnaissance

**Q5. Which tactic involves stealing collected data outside the organization?**

A. Discovery  
B. Persistence  
C. Exfiltration  
D. Weaponization

**Q6. Which tool is associated with credential dumping in the class examples?**

A. Mimikatz  
B. Suricata  
C. Shodan  
D. Mega.nz

**Q7. What is the main goal of breaking the attack chain?**

A. Generate more alerts  
B. Allow the attacker to move internally  
C. Interrupt the attack before the final objective  
D. Delete every SIEM log

### Answer Key

1. D — TTPs
2. A — DNS sinkholing
3. C — 18
4. B — Propagation
5. C — Exfiltration
6. A — Mimikatz
7. C — Interrupt the attack before the final objective

---

## 6. 🗺️ Final Memory Map

Pyramid of Pain:
Hash → IP → Domain → Artifacts → Tools → TTPs

UKC:
- Infiltration: Reconnaissance → Weaponization → Delivery → Social Engineering → Exploitation → Persistence → Defense Evasion → C2
- Propagation: Pivot → Discovery → Privilege Escalation → Execution → Credential Access → Lateral Movement
- Action: Collection → Exfiltration → Impact → Objectives

## 7. Final 30-Second Revision

- Pyramid of Pain: Higher layer = more attacker pain.
- Automate repetitive indicator blocking; investigate behaviours and TTPs.
- UKC = 18 tactics, 3 phases.
- Infiltration = Enter.
- Propagation = Expand.
- Action = Achieve.
- SOC goal = Understand the attack chain and interrupt it before the attacker reaches the final objective.
