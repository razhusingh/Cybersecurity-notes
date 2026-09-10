# DAY 5 - RAJU RECALL NOTES
# SOC Analyst L1
## Cyber Kill Chain + Hacking Methodology + Alert Reporting + Escalation + SOC Communication

---

# 1. 30-SECOND RECALL

## Cyber Kill Chain

- Lockheed Martin framework.
- 7-stage cyber attack lifecycle.
- Linear: Outside → Inside.
- Breaking a stage can stop the attack chain.

```text
Reconnaissance
↓
Weaponization
↓
Delivery
↓
Exploitation
↓
Installation
↓
C2
↓
Actions on Objectives
```

## Hacking Methodology

```text
Reconnaissance
↓
Scanning
↓
Gaining Access
↓
Maintaining Access
↓
Clearing Tracks
```

## Alert Reporting

- Document → Detection + Analysis + Conclusion + Action.
- SOC Golden Rule: **If it's not documented, it didn't happen.**
- Benefits → Audit trail + Handover + Incident Response + Legal protection + Better detections.

## Escalation

- Tier-1 → Identify + Triage + Document + Handover.
- Tier-1 does not fix incidents beyond authority.

Escalate for:

- Confirmed malicious activity
- Privileged account
- Critical asset
- Correlated alerts
- Data risk
- High/Critical severity

## SOC Communication

- Analyst → Analyst
- Analyst → IR
- Analyst → IT/Admin
- SOC → Management

**Goal:** Technical risk → Actionable information.

---

# 2. MUST REMEMBER

## 🔥 7 CYBER KILL CHAIN STAGES

| Stage | Recall |
|---|---|
| 1. Reconnaissance | Gather information |
| 2. Weaponization | Exploit + Payload |
| 3. Delivery | Send weapon |
| 4. Exploitation | Trigger vulnerability |
| 5. Installation | Establish persistence |
| 6. C2 | Remote control |
| 7. Actions | Final objective |

---

## 1. Reconnaissance

### Find

- Employee emails
- Domains/Subdomains
- Technologies
- Public profiles
- Leaked passwords

### Techniques

- Google Dorking
- WHOIS
- DNS Enumeration
- OSINT

### SOC Indicators

- Excessive DNS queries
- Scanning behaviour
- OSINT-based phishing patterns

---

## 2. Weaponization

```text
Exploit + Payload
```

- Payload = What runs after exploitation.
- Exploit = How vulnerability is abused.

Examples:

- Malicious PDF
- Word macro + reverse shell
- Exploit for unpatched service

SOC:

- File hash analysis
- Malware sandboxing
- Exploit signatures

---

## 3. Delivery

### Methods

- Phishing email
- Malicious attachment
- Drive-by website
- USB
- Compromised ads

### SOC Controls

- Email gateway filtering
- URL reputation
- Attachment sandboxing

---

## 4. Exploitation

**Vulnerability is triggered.**

Examples:

- Malicious link
- Buffer overflow
- Outdated plugin
- Macro execution

⭐ **No exploitation → No compromise**

---

## 5. Installation

**Persistence is established.**

Examples:

- Registry Run Keys
- Scheduled Tasks
- Startup Folders
- Backdoor users

SOC:

- EDR
- Registry monitoring
- Autorun analysis

---

## 6. Command & Control (C2)

```text
Compromised System
        ↕
Attacker Server
```

### Indicators

- Beaconing
- DNS tunneling
- HTTPS-based C2
- Abnormal outbound traffic
- Known bad IPs/domains

---

## 7. Actions on Objectives

Final attacker goal:

- Data theft
- Ransomware
- Credential dumping
- Lateral movement
- Financial fraud

---

# 3. CYBER KILL CHAIN vs HACKING METHODOLOGY

| Cyber Kill Chain | Hacking Methodology |
|---|---|
| Reconnaissance | Reconnaissance |
| Weaponization | Exploit Prep |
| Delivery | Payload Delivery |
| Exploitation | Gaining Access |
| Installation | Maintaining Access |
| C2 | Persistent Control |
| Actions | Post-Exploitation |

---

# 4. ALERT REPORTING

## What Must Be Documented?

```text
What was detected
        ↓
What was analyzed
        ↓
What conclusion was reached
        ↓
What action was taken/recommended
```

### Report Structure

```text
Summary
↓
Analysis
↓
Verdict
↓
Recommendation
```

### Good Report

- Clear
- Factual
- Evidence-based
- Defensible
- No unnecessary assumptions

### Why Reporting Matters

- Audit trail
- Shift handover
- Incident response
- Legal protection
- Detection improvement

⭐ **Bad reporting = Bad SOC Analyst, even if triage was correct.**

---

# 5. ALERT ESCALATION

## Tier-1 Role

```text
Detect
↓
Triage
↓
Investigate
↓
Document
↓
Escalate if required
```

### Escalate When

| Condition | Example |
|---|---|
| Confirmed malicious | Malware execution |
| Privileged account | Admin user |
| Critical asset | Server / DC |
| Multiple alerts correlated | Phishing + Execution |
| Data risk | Possible Exfiltration |
| Policy requires | High/Critical |

⭐ **Escalation is professionalism, not failure.**

---

## Escalation Note

Include:

```text
Reason
+
Evidence
+
Severity
+
Recommended Action
```

Evidence can include:

- Process tree
- Command line
- Destination domain

---

# 6. SOC COMMUNICATION

## Communication Principles

- Clear
- Factual
- No assumptions
- No panic language
- No blame

❌ `System hacked badly!!!`

✅ `Suspicious activity detected, under investigation.`

---

## Internal SOC Communication

Used for:

- Shift handover
- Escalation
- Collaboration

Example:

```text
Alert escalated to L2.
Endpoint pending isolation.
Monitoring ongoing.
```

---

## IT / Admin Communication

Used when **action is required**.

Example:

```text
Please isolate the endpoint as
suspicious activity was detected.
```

---

## Management Communication

Management wants:

```text
Impact + Status
```

Not raw technical logs.

Example:

```text
Suspicious activity detected on one
finance user system. No evidence of
data exfiltration so far. Incident
under investigation.
```

---

# 7. COMPLETE SOC WORKFLOW

```text
Alert Detected
↓
Alert Triage
↓
Alert Report Written
↓
Escalation (if needed)
↓
Clear Communication
↓
Action Taken
```

⭐ **Miss any step → SOC failure**

---

# 8. INTERVIEW Q&A

### Q1. What is Cyber Kill Chain?

**Ans:** Lockheed Martin framework describing the stages of a cyber attack.

### Q2. How many stages are in Cyber Kill Chain?

**Ans:** 7.

### Q3. Name the 7 stages.

**Ans:** Reconnaissance → Weaponization → Delivery → Exploitation → Installation → C2 → Actions on Objectives.

### Q4. What is Reconnaissance?

**Ans:** Gathering information about the target.

### Q5. What is Weaponization?

**Ans:** Preparing an exploit and malicious payload.

### Q6. What is Delivery?

**Ans:** Sending the weapon/payload to the victim.

### Q7. What is Exploitation?

**Ans:** Triggering a vulnerability.

### Q8. What is Installation?

**Ans:** Establishing persistence on the victim system.

### Q9. What is C2?

**Ans:** Communication/control channel between compromised system and attacker.

### Q10. What is Alert Reporting?

**Ans:** Documenting what was detected, analyzed, concluded and action taken/recommended.

### Q11. What is the SOC Golden Rule for reporting?

**Ans:** **If it's not documented, it didn't happen.**

### Q12. When should Tier-1 escalate?

**Ans:** Confirmed malicious activity, privileged account, critical asset, correlated alerts, data risk or required high/critical severity.

### Q13. What is the role of Tier-1 during escalation?

**Ans:** Identify, triage, document and correctly hand over; not fix incidents beyond Tier-1 authority.

### Q14. What are SOC communication principles?

**Ans:** Clear, factual, no assumptions, no panic language, no blame.

### Q15. What does management need from SOC?

**Ans:** Impact and current status.

---

# 9. QUESTION PAPER MODE

1. What is Cyber Kill Chain?
2. Who created the Cyber Kill Chain framework?
3. Name all 7 Cyber Kill Chain stages.
4. What happens during Reconnaissance?
5. What is Weaponization?
6. What is the difference between Exploit and Payload?
7. What are common Delivery methods?
8. What happens during Exploitation?
9. What is Installation/Persistence?
10. What is C2 and what are its SOC indicators?
11. What are Actions on Objectives?
12. Differentiate Cyber Kill Chain and Hacking Methodology.
13. What is Alert Reporting?
14. What information should an alert report contain?
15. Why is alert reporting important in a SOC?
16. What is Tier-1's role during escalation?
17. When should a Tier-1 analyst escalate an alert?
18. What should an escalation note contain?
19. What are the principles of SOC communication?
20. How should SOC communicate with Management?
21. Explain the complete Alert → Action SOC workflow.

---

# 10. ANSWER KEY

**1.** Framework describing the stages of a cyber attack.

**2.** Lockheed Martin.

**3.**

```text
Reconnaissance
→ Weaponization
→ Delivery
→ Exploitation
→ Installation
→ C2
→ Actions on Objectives
```

**4.** Target information gathering using methods such as OSINT, DNS enumeration and WHOIS.

**5.** Preparing exploit + payload.

**6.**

- Exploit = How vulnerability is abused.
- Payload = What executes after exploitation.

**7.** Phishing email, malicious attachment, drive-by website, USB, compromised ads.

**8.** Vulnerability is triggered.

**9.** Malware establishes persistence so access remains after restart.

**10.** Compromised system communicates with attacker server; indicators include beaconing, DNS tunneling, HTTPS C2 and abnormal outbound traffic.

**11.** Final attacker objectives such as data theft, ransomware, credential dumping, lateral movement or financial fraud.

**12.**

- Kill Chain = 7-stage attacker lifecycle.
- Hacking Methodology = Practical execution flow: Recon → Scanning → Gaining Access → Maintaining Access → Clearing Tracks.

**13.** Formal documentation of detection, analysis, conclusion and action.

**14.** Summary, analysis, verdict and recommendation.

**15.** Audit trail, handover, incident response, legal protection and detection improvement.

**16.** Identify, triage, investigate, document and hand over when required.

**17.** Confirmed malicious activity, privileged account, critical asset, correlated alerts, data risk or policy-required high/critical severity.

**18.** Escalation reason, evidence, severity and recommended action.

**19.** Clear, factual, no assumptions, no panic language, no blame.

**20.** Communicate impact + status rather than raw technical logs.

**21.**

```text
Alert Detected
→ Triage
→ Report
→ Escalation if needed
→ Clear Communication
→ Action Taken
```

---
