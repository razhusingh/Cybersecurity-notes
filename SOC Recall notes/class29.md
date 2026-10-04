# SOC Analyst L1 — Class 29
---

# ⚡ 30-SECOND RECALL

**SOAR = Security Orchestration, Automation & Response**

SOAR connects security tools and helps the SOC:

    CONNECT
       ↓
    AUTOMATE
       ↓
    RESPOND

Commonly connected tools:

- SIEM
- EDR
- Firewall
- IAM

Main idea:

    Many Security Tools
           ↓
          SOAR
           ↓
    One Unified Interface
           ↓
    Faster Investigation & Response

---

# 🔥 MUST REMEMBER

## 1. Three Pillars of SOAR

### Orchestration

Connects and coordinates different security technologies.

Uses:

- Integrations
- Apps
- Connectors
- REST APIs

### Automation

Performs tasks without continuous human intervention.

Uses:

- Playbooks
- Workflows
- Triggers
- If/Else logic

### Response

Allows security actions to be performed through the connected tools.

---

# 2. Orchestration

SOAR acts as the:

    Glue

between security tools.

Example:

    SOAR
      ↓
    REST API
      ↓
    Firewall
      ↓
    Block IP

---

# 3. Playbooks / Workflows

A playbook is a:

    Step-by-Step Incident Workflow

It can contain:

    IF / ELSE

logic.

### Trigger

A trigger starts the playbook.

Example:

    SIEM detects phishing
           ↓
    Playbook starts

---

# 4. SOAR Response Example

### VPN Brute Force

    VPN Brute Force Detected
             ↓
       Block IP on Firewall
             ↓
       Disable User in IAM
             ↓
          Open Ticket
             ↓
       Add Incident Details

---

# 5. Threat Intelligence

SOAR can ingest:

    Threat Intelligence Feeds

It can compare internal alert information with threat intelligence.

Purpose:

    Enrich Incident Context

---

# 6. Case Management

If automation cannot completely resolve an incident:

    Incident
       ↓
      Case

A case can contain:

- Full audit trail
- Automated actions already performed
- Timeline
- Evidence lockers
- Files
- Hashes
- Collaboration tools

---

# 7. Alert Fatigue

Traditional SOCs can receive:

    Millions of Logs
          ↓
      Many Alerts
          ↓
    False Positives
          ↓
    Analyst Burnout

Important:

**IOC = Indicator of Compromise**

### SOAR Solution

SOAR can:

- Deduplicate
- Correlate
- Filter known benign noise

Flow:

    Many Alerts
         ↓
        SOAR
         ↓
    Filter / Correlate
         ↓
    High-Fidelity Incidents
         ↓
    Human Analyst

---

# 8. Tool Fragmentation — Swivel-Chair Effect

An analyst may have to switch between:

- Email Gateway
- Threat Intelligence Portal
- Active Directory
- EDR Console

This creates:

    Context Switching
          ↓
    Slower Response

### SOAR Solution

SOAR connects tools through:

    APIs

and provides:

    Single Pane of Glass

The analyst can work from SOAR while SOAR communicates with the other tools.

---

# 9. MTTD / MTTR

Manual investigation can involve:

- Copy-pasting IP addresses
- Opening tickets
- Waiting for user confirmations

This can stretch an incident from:

    Minutes → Days

SOAR performs repetitive tasks at:

    Machine Speed

Example:

    Manual Work
       ↓
    45 minutes

    SOAR Playbook
       ↓
    Less than 5 seconds

This can reduce:

    MTTR

---

# 10. Traditional SOC vs SOAR

| Feature | Traditional SOC | SOAR-Enabled SOC |
|---|---|---|
| Triage Time | Minutes to Hours | Seconds |
| Enrichment | Manual lookups | Automated enrichment |
| Playbook Execution | Static PDF documents | Dynamic Code / Workflows |
| Human Role | Data gatherer / button clicker | Decision maker / Threat Hunter |
| Tool Ecosystem | Siloed, disconnected consoles | Orchestrated, unified API mesh |

---

# 11. Phishing SOAR Playbook

Main flow:

    Trigger & Ingestion
            ↓
    Enrichment & Triage
            ↓
    Analysis & Correlation
            ↓
    Response & Mitigation
            ↓
    Post-Incident & Reporting

---

# 12. Trigger & Ingestion

Possible triggers:

- SIEM / Email Alert
- User Reporting

Then:

    Playbook Activated

Alert information is parsed for:

- URL
- Sender
- Recipient
- Attachment hashes

---

# 13. Enrichment & Triage

## Threat Intelligence Lookup

Checks:

    URL / IP Reputation

Using:

- VirusTotal
- Cyberint

## Active Directory

Checks:

- User Profile
- VIP Status

## EDR

Checks:

    Endpoint Posture

Then asks:

    Is Alert High Fidelity?

### NO

    False Positive Dismissal

### YES

    Continue to Analysis

---

# 14. Analysis & Correlation

The playbook:

- Correlates IOCs across the network
- Analyzes the attachment in a sandbox
- Checks past incident history

Then asks:

    Is It Malicious?

### NO

    Close Case as Benign

### YES

    Continue to Response

---

# 15. Response & Mitigation

Two response tracks:

    FULL AUTO
    SEMI-AUTO

## Full Auto

Used for:

    High Confidence

Actions:

- Block URL on Firewall
- Update EDR Policies
- Reset User Password

## Semi-Auto

Used when:

    Human Review Required

The analyst reviews the mitigation steps.

Possible actions:

- Execute mitigation steps
- Delete email enterprise-wide
- Isolate host via EDR

---

# 16. Post-Incident & Reporting

After response:

1. Update ticketing system
2. Generate incident report
3. Share threat intelligence
4. Close case

Ticketing example:

    ServiceNow

---

# ⭐ INTERVIEW Q&A

## Q1. What is SOAR?

**Answer:**  
SOAR stands for Security Orchestration, Automation & Response. It connects security tools and helps automate security operations and response.

## Q2. What are the three pillars of SOAR?

**Answer:**

    Orchestration
    Automation
    Response

## Q3. What is orchestration?

**Answer:**  
Coordinating different security technologies so they work together.

## Q4. What is a playbook?

**Answer:**  
A step-by-step workflow used to handle an incident.

## Q5. What is a trigger?

**Answer:**  
An event that starts a playbook.

## Q6. How does SOAR help with alert fatigue?

**Answer:**  
It can deduplicate, correlate and filter known benign noise.

## Q7. What is the Swivel-Chair Effect?

**Answer:**  
Constantly switching between different security consoles during an investigation.

## Q8. How does SOAR reduce response time?

**Answer:**  
It automates repetitive tasks at machine speed.

## Q9. What is the difference between Full Auto and Semi-Auto?

**Answer:**  
Full Auto performs actions automatically for high-confidence incidents. Semi-Auto requires human review before mitigation.

## Q10. What are the five stages of the phishing playbook?

**Answer:**

1. Trigger & Ingestion
2. Enrichment & Triage
3. Analysis & Correlation
4. Response & Mitigation
5. Post-Incident & Reporting

---

# 🧠 SOC ANALYST MINDSET

Think:

    ALERT
      ↓
    ENRICH
      ↓
    ANALYZE
      ↓
    DECIDE
      ↓
    RESPOND
      ↓
    DOCUMENT
      ↓
    CLOSE

### Remember

SOAR does not necessarily remove the analyst.

It can automate repetitive work while keeping the analyst involved in important decisions.

---

# 📝 QUESTION PAPER MODE

1. What is SOAR?
2. What are the three pillars of SOAR?
3. What is orchestration?
4. What is a playbook?
5. What is a trigger?
6. How does SOAR help with alert fatigue?
7. What is the Swivel-Chair Effect?
8. How does SOAR reduce MTTR?
9. What is the difference between Full Auto and Semi-Auto?
10. What are the five stages of the phishing SOAR playbook?
11. What happens during enrichment and triage?
12. What happens during analysis and correlation?
13. What happens during post-incident reporting?

---

# ✅ ANSWER KEY

1. Security Orchestration, Automation & Response.
2. Orchestration, Automation and Response.
3. Coordinating different security technologies.
4. A step-by-step incident-handling workflow.
5. An event that starts a playbook.
6. By deduplicating, correlating and filtering benign noise.
7. Constantly switching between different security consoles.
8. By automating repetitive tasks at machine speed.
9. Full Auto = automatic high-confidence response; Semi-Auto = human review required.
10. Trigger & Ingestion → Enrichment & Triage → Analysis & Correlation → Response & Mitigation → Post-Incident & Reporting.
11. Threat intelligence, Active Directory and EDR checks are performed.
12. IOCs are correlated, attachments are analyzed and past incident history is checked.
13. Ticket is updated, incident report is generated, threat intelligence is shared and the case is closed.

---

# 🧩 FINAL MEMORY MAP

    SOAR
      │
      ├── ORCHESTRATION
      │      └── Connect Tools
      │
      ├── AUTOMATION
      │      └── Playbooks / Workflows
      │
      └── RESPONSE
             └── Security Actions

    PHISHING:
    
    TRIGGER
       ↓
    ENRICH
       ↓
    ANALYZE
       ↓
    RESPOND
       ↓
    REPORT
       ↓
    CLOSE

---

# 🔥 30-SECOND FINAL REVISION

**SOAR** = Security Orchestration, Automation & Response

**Three pillars** = Orchestration + Automation + Response

**Playbook** = Step-by-step workflow

**Trigger** = Starts playbook

**REST API** = Helps connect SOAR with security tools

**Alert Fatigue** = Too many alerts / false positives

**Swivel-Chair Effect** = Switching between many consoles

**Single Pane of Glass** = Unified interface

**Full Auto** = High-confidence automatic response

**Semi-Auto** = Human review

**Phishing Flow**:

    Trigger
      ↓
    Enrich
      ↓
    Analyze
      ↓
    Respond
      ↓
    Report
      ↓
    Close

---
