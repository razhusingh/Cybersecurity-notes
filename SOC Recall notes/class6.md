# DAY 6 — RAJU RECALL NOTES
## Malware

---

# 1. 30-SECOND RECALL

**Malware = Malicious Software** designed to:
- Steal data
- Disrupt systems
- Gain unauthorized access
- Spy on users
- Encrypt files for ransom

### 6 Important Types

| Malware | Core Idea | Main Goal |
|---|---|---|
| **Virus** | Attaches to legitimate file; needs execution | Infect files |
| **Worm** | Self-propagates over network | Spread rapidly |
| **Trojan** | Disguised as legitimate software | Backdoor |
| **Ransomware** | Encrypts victim files | Ransom |
| **Spyware** | Secretly collects information | Steal data |
| **Rootkit** | Hides malware/activity | Remain hidden |

**Golden Difference:**
> Virus needs user interaction → Worm spreads automatically.

:contentReference[oaicite:0]{index=0}

---

# 2. MUST REMEMBER

## 🔴 Virus
**Flow:** Infected file → User runs → Virus executes → Spreads to files

**Example:** Infected `.exe` via USB

**SOC Indicators:**
- Unknown process spawning
- Suspicious file modification
- Antivirus alert

:contentReference[oaicite:1]{index=1}

---

## 🟠 Worm

- No user action required
- Self-propagates through networks
- Example: **WannaCry → SMB vulnerability**

**SOC Indicators:**
- Sudden network traffic spike
- Same payload on multiple hosts
- Lateral scanning

:contentReference[oaicite:2]{index=2}

---

## 🟡 Trojan

**Definition:** Malware disguised as legitimate software.

**Example:** Fake "Free Cracked Software.exe"

**Can:**
- Open backdoor
- Steal data
- Install additional malware

**SOC Indicators:**
- Unusual outbound traffic
- Unknown services
- Suspicious startup entries

:contentReference[oaicite:3]{index=3}

---

## 🔴 Ransomware

**Definition:** Encrypts victim files and demands ransom.

### Attack Flow
`Phishing → User clicks attachment → Malware installs → Files encrypted → Ransom note`

**SOC Indicators:**
- Mass file renaming
- High CPU usage
- Shadow copy deletion
- Unusual encryption activity

:contentReference[oaicite:4]{index=4}

---

## 🔵 Spyware

**Definition:** Secretly collects user information.

**Can steal:**
- Passwords
- Banking information
- Screenshots
- Keystrokes → Keylogger

**SOC Indicators:**
- Strange outbound connections
- DNS queries to unknown domains
- Data-exfiltration alerts

:contentReference[oaicite:5]{index=5}

---

## ⚫ Rootkit

**Definition:** Malware designed to hide other malware.

**Hides:**
- Processes
- Files
- Registry entries

**SOC Indicators:**
- User-mode vs kernel-mode mismatch
- Integrity-check failures
- Unusual driver loads

:contentReference[oaicite:6]{index=6}

---

# 3. QUICK COMPARISON

| Type | User Needed? | Auto Spread? | Main Goal |
|---|---|---|---|
| Virus | Yes | No | Infect files |
| Worm | No | Yes | Spread |
| Trojan | Yes | No | Backdoor |
| Ransomware | Yes | Sometimes | Encrypt files |
| Spyware | Yes | No | Steal data |
| Rootkit | No | No | Hide malware |

:contentReference[oaicite:7]{index=7}

---

# 4. SOC ANALYST MINDSET

When a malware alert appears, ask:

1. **Is this malware delivery?**
2. **Is there persistence?**
3. **Is lateral movement happening?**
4. **Is data being exfiltrated?**
5. **Is there encryption/ransomware behavior?**

### SOC L1 Core Job
**Detect → Validate → Escalate**

:contentReference[oaicite:8]{index=8}

---

# 5. INTERVIEW Q&A

### Q1. What is malware?
Malicious software designed to steal, disrupt, spy, gain unauthorized access, or encrypt data.

### Q2. Virus vs Worm?
Virus needs user interaction; worm self-propagates.

### Q3. What is a Trojan?
Malware disguised as legitimate software.

### Q4. What is ransomware?
Malware that encrypts files and demands ransom.

### Q5. What is spyware?
Malware that secretly collects user information.

### Q6. What is a rootkit?
Malware designed to hide malicious activity/files/processes.

### Q7. Give a worm example.
WannaCry.

### Q8. Ransomware SOC indicators?
Mass file renaming, encryption activity, shadow-copy deletion, high CPU.

### Q9. Trojan SOC indicators?
Unknown services, suspicious startup entries, unusual outbound traffic.

### Q10. What does SOC L1 do with a malware alert?
**Detect → Validate → Escalate.**

---

# 6. QUESTION PAPER MODE

1. What is malware?
2. Name six common malware types.
3. Define a virus.
4. How does a virus spread?
5. Virus vs worm?
6. What is a worm?
7. Why is WannaCry considered a worm?
8. What is a Trojan?
9. What can a Trojan do?
10. Define ransomware.
11. Write the ransomware attack flow.
12. Give four ransomware SOC indicators.
13. What is spyware?
14. What information can spyware steal?
15. Define rootkit.
16. Why are rootkits difficult to detect?
17. Write the six malware types with their primary goals.
18. What questions should a SOC analyst ask when a malware alert appears?
19. What are the three core responsibilities of SOC L1?

---

# 7. ANSWER KEY

1. Malicious software.
2. Virus, Worm, Trojan, Ransomware, Spyware, Rootkit.
3. Malware attached to a legitimate file.
4. Executes with the infected file and spreads to other files.
5. Virus needs user interaction; worm self-propagates.
6. Malware that automatically spreads over networks.
7. It spread automatically using an SMB vulnerability.
8. Malware disguised as legitimate software.
9. Backdoor, data theft, additional malware installation.
10. Malware that encrypts files and demands ransom.
11. Phishing → Click → Install → Encrypt → Ransom note.
12. Mass renaming, high CPU, shadow-copy deletion, encryption activity.
13. Malware that secretly collects user information.
14. Passwords, banking info, screenshots, keystrokes.
15. Malware designed to hide other malware.
16. It hides processes, files and registry entries.
17. Virus–infect, Worm–spread, Trojan–backdoor, Ransomware–encrypt, Spyware–steal, Rootkit–hide.
18. Delivery? Persistence? Lateral movement? Exfiltration? Encryption?
19. Detect → Validate → Escalate.

---
