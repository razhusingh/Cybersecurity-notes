Day 1 – From Zero to SOC Analyst L1 

# 🚀 30-Second Recall
- SOC = Security Operations Center.
- SOC monitors, detects and responds to cyber threats 24×7.
- SOC = Detection & Response.
- SOC Analyst L1 = First responder.
- L1 performs Alert Triage.
- L2 performs Deep Investigation.
- L3 performs Threat Hunting & Incident Response support.
- SOC ≠ NOC ≠ IR Team.
- SIEM = Collects & correlates logs.
- EDR = Endpoint detection & response.
- IOC = Indicator of Compromise.
- Alert → Triage → Investigation → Escalation/Closure.
- True Positive = Real attack.
- False Positive = Benign activity.
- Check logs before & after alert.
- Investigate Source IP, User, Process, Timeline.
- Escalate when compromise is suspected.
- Common attacks: Phishing, Malware, Ransomware, Brute Force.
- Event ID 4625 = Failed Login.
- Event ID 4740 = Account Lockout.
- Think like a defender, not an attacker.

# 📌 Must Remember
SOC vs NOC vs IR

- SOC

Detects & monitors security threats.

- NOC

Monitors network availability & performance.

- IR Team

Responds to confirmed security incidents.
SOC Levels

L1
- Monitor
- Triage
- Validate
- Escalate

L2
- Deep Investigation
- Malware Analysis
- Threat Correlation

L3
- Threat Hunting
- Incident Response
- Advanced Analysis

# Alert Triage Flow
```
Alert

↓

Read Alert

↓

Collect Logs

↓

Analyze Context

↓

True Positive / False Positive

↓

Escalate or Close
```

True Positive Indicators
- Malicious IP
- Privilege Escalation
- Data Exfiltration
- Multiple Failed Logins
- Successful Login after Failures

False Positive Examples
- Legitimate Admin Activity
- Scheduled Tasks
- Automated Scanners
- Poor SIEM Rules

Important Tools
- SIEM (Splunk, Sentinel, QRadar)
- EDR/XDR (CrowdStrike, Defender)
- VirusTotal
- AbuseIPDB
- MITRE ATT&CK
- ServiceNow
- Jira

Important Event IDs
- 4625 → Failed Login
- 4740 → Account Lockout

# 💼 Interview Q&A
1. What is a SOC?

A Security Operations Center that continuously monitors, detects, investigates and responds to cyber threats.

2. What is the role of a SOC Analyst L1?

Monitor alerts, perform initial triage, investigate logs, validate alerts and escalate genuine threats.

3. Difference between SOC, NOC and IR Team?
- SOC → Detects threats
- NOC → Monitors network
- IR → Responds to confirmed incidents

4. What is Alert Triage?

The process of determining whether an alert is a True Positive or False Positive.

5. What is a True Positive?

A genuine security incident requiring action.

6. What is a False Positive?

A legitimate activity incorrectly identified as malicious.

7. What should an L1 analyst check first?

Alert severity, affected asset, source IP, user, logs and timeline.

8. Difference between SIEM and EDR?

- SIEM analyzes logs from multiple sources.
- EDR monitors and responds at the endpoint level.

9. Name common attacks seen in a SOC.
- Phishing
- Malware
- Ransomware
- Brute Force

10. Which Event ID indicates failed login?

4626

11. Which Event ID indicates account lockout?
4740

# SOC Analyst Mindset

Whenever an alert appears, ask yourself:
- Is this malicious?
- Is the source IP trusted?
- Is the user legitimate?
- Is this normal behavior?
- What happened before the alert?
- What happened after the alert?
- Is there any IOC?
- Should this be escalated?

SOC L1 Rule:
- Detect → Validate → Document → Escalate

# 📝 Question Paper Mode
1. What is a SOC?

2. What is the primary role of a SOC Analyst L1?

3. Difference between SOC, NOC and IR Team.

4. What is Alert Triage?

5. Difference between True Positive and False Positive.

6. What should an analyst investigate before escalating an alert?

7. Difference between SIEM and EDR.

8. Name four common cyber attacks monitored in a SOC.

9. Which Event ID indicates Failed Login?

10. Which Event ID indicates Account Lockout?

11. Name common Threat Intelligence tools.

12. Explain the Alert Triage workflow.

13. When should an alert be escalated?

14. What are common examples of False Positives?

15. Why should a SOC analyst think like a defender?

#✅ Answer Key

1. Security Operations Center that monitors, detects, investigates and responds to cyber threats.

2. Monitor alerts, perform triage, investigate, document and escalate.

3. 
- SOC → Security monitoring
- NOC → Network monitoring
- IR → Incident response

4. Determining whether an alert is a True Positive or False Positive.

5. 
- True Positive → Real attack
- False Positive → Benign activity

6. 
- Source IP
- User
- Logs
- Timeline
- Severity
- Context

7. 
- SIEM → Log collection & correlation
- EDR → Endpoint monitoring & response

8. 
- Phishing
- Malware
- Ransomware
- Brute Force

9. Event ID 4625.

10. Event ID 4740.

11.
- virusTotal
- AbuseIPDB
- MITRE ATT&CK

12. Alert → Collect Logs → Analyze Context → True/False Positive → Escalate or Close.

13. When evidence indicates a genuine compromise or suspicious activity.

14. 
- Legitimate admin activity
- Scheduled tasks
- Automated scans
- Poorly tuned SIEM rules

15. Because the goal is to detect attacker behavior, validate alerts and protect the organization before damage occurs.