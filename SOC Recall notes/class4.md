# SOC Analyst L1 – Day 4 

# 30-Second Recall
- TTP = Tactics + Techniques + Procedures

- Tactics = WHY attacker performs an action (Goal)

- Techniques = HOW attacker performs the attack (Method)

- Procedures = Exact implementation (Tools, Commands, Scripts)

- MITRE ATT&CK = Maps attacker behavior

- IOC = Observable evidence of compromise

- TTP = Attacker behavior

- IOC = Attacker footprints

- Network IOC = IP, Domain, C2, Ports

- Host IOC = Process, Registry, Services, Scheduled Tasks

- File IOC = Hash, Filename, File Size

- Email IOC = Sender, Subject, URL, Headers

- IOC Confidence = Low → Medium → High → Very High

- Never trust a single IOC

- IOC = What happened

- TTP = How it happened

- IOC + TTP = Better Detection

- IOC Flow = Detect → Alert → Validate → Map TTP → TP/FP → Escalate/Close

- Alert Triage = Separate real attacks from noise

- Good Triage = Fast, Accurate, Prioritized Investigation
 
# Must Remember Points
# TTP (Tactics, Techniques & Procedures)

Purpose
- Describe attacker behavior
- Explain how and why an attack happened
- Detect attacks even when IOCs change
- Understand attacker intent
- Improve detections and response playbooks

Why TTP is Important
- IOC tells what happened.

TTP tells:
- How the attack happened
- Why the attacker performed it
SOC analysts focus more on attacker behavior than only indicators.

# Tactics (WHY)
- Represents the attacker's goal.

Common Tactics
- Initial Access
- Execution
- Persistence
- Privilege Escalation
- Defense Evasion
- Credential Access
- Lateral Movement
- Exfiltration

Tactic Meanings
- Initial Access → First entry
- Execution → Run malicious code
- Persistence → Stay in the system
- Privilege Escalation → Gain admin rights
- Defense Evasion → Avoid security tools
- Credential Access → Steal credentials
- Lateral Movement → Move to another system
- Exfiltration → Steal data

# Techniques (HOW)
Specific methods attackers use to achieve a tactic.

Example
```
Credential Access

↓

Techniques
- Keylogging
- Credential Dumping (LSASS)
- Browser Password Theft
- Phishing
One tactic can have multiple techniques.
```
# Procedures (EXACT IMPLEMENTATION)

Real-world execution of a technique using:
- Tools
- Commands
- Scripts
- Timing
Example
```
Technique

Credential Dumping

↓

Procedure

Use procdump to dump LSASS memory.
```
# MITRE ATT&CK

MITRE ATT&CK is:
- Global attacker knowledge base
- Built around Tactics & Techniques
- Used by SOC, SIEM, EDR and XDR
- Helps map attacker behavior
- Essential framework for SOC analysts

# IOC (Indicators of Compromise)
IOC = Observable evidence showing a system may be compromised.

IOC Sources
- Logs
- Network Traffic
- Endpoint Activity
- Email Headers
- File Systems

IOC Helps To
- Trigger SIEM Alerts
- Confirm Malicious Activity
- Correlate Attacks
- Speed Response
- Write Incident Reports

# IOC Categories
🌐 Network IOC

Examples
- Malicious IP
- Suspicious Domain
- C2 Communication
- Unusual Ports

Seen In
- Firewall Logs
- Proxy Logs
- DNS Logs
- IDS/IPS

💻 Host / Endpoint IOC

Examples
- Suspicious Process
- Unexpected Services
- Registry Changes
- Scheduled Tasks

Seen In
- EDR/XDR
- Windows Event Logs
- Sysmon
- Linux Audit Logs

📂 File IOC

Examples
- MD5
- SHA256
- File Name Pattern
- File Size Anomaly

Seen In
- Antivirus
- EDR
- Email Security Gateway
- Sandbox

📧 Email IOC

Examples
- Malicious Sender
- Phishing Subject
- Malicious URL
- Header Anomalies

Seen In

- Microsoft Defender
- Proofpoint
- Mimecast
- Email Security Tools
- User Reports

IOC Confidence Levels
|Level | Example  |
|------|----------|
|Low |Single Suspicious IP |
|Medium	|Known Phishing Domain |
|High |Malware Hash + Execution |
|Very High |Multiple Correlated IOCs |

Golden Rule

➡️ Never rely on a single IOC.

Always correlate multiple IOCs before confirming an incident.

# IOC vs TTP
IOC
- Evidence
- What Happened
- Short-lived
- Easy to Change
- Used for Alerts

TTP
- Behavior
- How it Happened
- Long-lived
- Hard to Change
- Used for Detection Logic

# SOC analayst mindset
SOC investigation workflow
```
Security Event Occurs
        │
        ▼
Logs Generated
(OS / Firewall / EDR / Email / Cloud)
        │
        ▼
SIEM / EDR Generates Alert
        │
        ▼
L1 SOC Receives Alert
        │
        ▼
Identify IOC(s)
(IP / Domain / Hash / Process / User / URL)
        │
        ▼
Validate Alert
(True Positive / False Positive)
        │
        ▼
Collect Related Evidence
• SIEM Logs
• EDR/XDR
• Firewall Logs
• DNS Logs
• Proxy Logs
• Windows Event Logs
• Email Logs
        │
        ▼
Map to MITRE ATT&CK
(Tactic → Technique → Procedure)
        │
        ▼
Determine
• Severity
• Impact
• Scope
• Affected Assets
        │
        ▼
Decision
        │
 ┌───────────────┴───────────────┐
 │                               │
 ▼                               ▼
False Positive             True Positive
 │                               │
Close Alert                 Escalate to L2 / IR
                             │
                             ▼
                     Incident Response
                     
```
During Investigation Ask Yourself
- Which IOC triggered the alert?
- Which MITRE Tactic matches?
- Which Technique was used?
- Which logs should I investigate?
- Is this True Positive or False Positive?
- What is the business impact?
- Should I escalate or close the alert?

# Interview Q&A
Q1. What is Alert Triage?

Answer: The process of validating, prioritizing and deciding whether a security alert requires investigation.

Q2. Why is Alert Triage important?

Answer:
- Removes false positives
- Prioritizes critical alerts
- Reduces analyst workload
- Speeds up incident response

Q3. What information should be checked during Alert Triage?

Answer:
- Source & Destination
- User/Host
- Time
- Triggering IOC
- Related Logs
- Asset Criticality

Q4. Difference between Severity and Priority?

Answer:
- Severity = How serious the threat is.
- Priority = How quickly it should be handled.

Q5. What is a True Positive?

Answer: A genuine security incident requiring investigation.

Q6. What is a False Positive?

Answer: An alert that appears malicious but is actually legitimate.

Q7. Why is IOC correlation important?

Answer: Multiple correlated IOCs increase confidence and reduce false positives.

Q8. Why do SOC analysts use MITRE ATT&CK?

Answer: To understand attacker behavior, map techniques, improve detection and support investigations.

Q9. Difference between IOC and TTP?

Answer:
- IOC = Evidence (What happened)
- TTP = Attacker behavior (How it happened)

Q10. Explain the SOC investigation workflow.

Answer:
- Event → Logs → Alert → IOC → Validation → Evidence → MITRE Mapping → Severity → Decision → Escalation/Closure.

# Question Paper Mode
1. What does TTP stand for?

2. Why is TTP more useful than only relying on IOCs?

3. What is a Tactic?

4. What is a Technique?

5. What is a Procedure?

6. What is the MITRE ATT&CK Framework?

7. What is an IOC?

8. Name the four IOC categories.

9. Give examples of Network IOCs.

10. Give examples of Host IOCs.

11. Give examples of File IOCs.

12. Give examples of Email IOCs.

13. What are the IOC Confidence Levels?

14. Why should a SOC analyst correlate multiple IOCs?

15. Differentiate between IOC and TTP.

16. What is Alert Triage?

17. Why is Alert Triage important?

18. What should be verified during Alert Triage?

19. Differentiate Severity and Priority.

20. Explain the SOC Investigation Workflow.

21. What is a True Positive?

22. What is a False Positive?

23. Why is MITRE ATT&CK important for SOC analysts?

24. Why is IOC correlation important?

25. Explain the complete IOC → Incident lifecycle.

# Answer Key

1. Tactics, Techniques and Procedures.

2. TTP focuses on attacker behavior, which changes less frequently than IOCs and helps detect similar attacks.

3. A Tactic is the attacker's objective or goal.

4. A Technique is the method used to achieve a tactic.

5. A Procedure is the exact implementation of a technique using specific tools or commands.

6. MITRE ATT&CK is a framework that maps attacker tactics and techniques to improve detection and investigation.

7. An IOC is observable evidence indicating possible system compromise.

8. 
- Network IOC
- Host IOC
- File IOC
- Email IOC

9. 
- Malicious IP
- Suspicious Domain
- C2 Communication
- Unusual Ports

10. 
- Suspicious Process
- Unexpected Service
- Registry Changes
- Scheduled Tasks

11. 
- MD5/SHA256 Hash
- Filename
- File Size Anomaly

12. 
- Malicious Sender
- Phishing Subject
- Malicious URL
- Email Header Anomaly

13. 
- Low
- Medium
- High
- Very High

14. Because a single IOC may be a false positive; multiple correlated IOCs provide stronger evidence.

15. 
- IOC = Evidence (What happened)
- TTP = Behavior (How it happened)

16. Alert Triage is the process of validating and prioritizing security alerts.

17.
- Remove false positives
- Prioritize incidents
- Speed investigation
- Reduce workload

18. 
- Source/Destination
- User/Host
- Time
- IOC
- Related Logs
- Asset Criticality

19. 
- Severity = Threat seriousness
- Priority = Response urgency

20.
- Event → Logs → Alert → IOC → Validation → Evidence → MITRE → Severity → - Decision → Escalate/Close.

21. A True Positive is a genuine security incident.

22. A False Positive is a benign event incorrectly flagged as malicious.

23. MITRE ATT&CK helps analysts understand attacker behavior, map techniques and improve detections.

24. IOC correlation improves confidence and reduces false positives.

25. IOC Detected → Alert Generated → Alert Triage → IOC Correlation → MITRE Mapping → Investigation → Incident Confirmation → Response & Escalation.