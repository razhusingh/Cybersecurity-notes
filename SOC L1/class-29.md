# SOC Analyst L1 — Class 29

## SOAR — Security Orchestration, Automation & Response

---

# 1. What is SOAR?

**SOAR = Security Orchestration, Automation & Response**

SOAR is a tool that unifies the security tools used in a SOC.

Instead of an analyst switching between different security consoles, SOAR allows them to operate multiple security tools from one interface.

### Tools that can be connected

- SIEM
- EDR
- Firewall
- IAM
- Other security tools

### SOAR also provides

- Ticketing
- Case management
- Incident documentation
- Incident tracking
- Incident resolution

### Easy Understanding

Without SOAR:

    SIEM → Check
    EDR → Check
    Firewall → Check
    IAM → Check

The analyst keeps switching between tools.

With SOAR:

    SIEM
      +
    EDR
      +
    Firewall
      +
    IAM
      ↓
     SOAR
      ↓
    One Interface

---

# 2. Three Pillars of SOAR

SOAR depends on three main pillars:

    ORCHESTRATION
          +
    AUTOMATION
          +
      RESPONSE

---

# 3. Security Orchestration

## What is Orchestration?

Orchestration is the ability to coordinate different security technologies so they can work together seamlessly.

It acts as the:

    Glue

between security tools.

### Examples of connected technologies

- SIEM
- EDR
- Firewall
- IAM

---

## Integrations and Plug-ins / Apps

SOAR platforms use:

- Pre-built apps
- Integration packs
- Connectors

These allow SOAR to communicate with different security products.

---

## API Centricity

SOAR relies heavily on:

    REST APIs

For example, if SOAR needs to block an IP address, it can send an API request to the firewall.

Example:

    POST /api/v1/block_list

### Easy Flow

    SOAR
      ↓
    API Request
      ↓
    Firewall
      ↓
    Block IP

---

# 4. Security Automation

## What is Automation?

Automation means:

    Executing tasks
    without human intervention

SOAR uses:

    Playbooks / Workflows

to automate incident-handling steps.

---

## Playbooks / Workflows

Playbooks are:

- Step-by-step visual flowcharts
- Used to decide how an incident should be handled
- Can contain conditional logic

Example:

    IF condition is true
          ↓
       Action A

    ELSE
          ↓
       Action B

So playbooks can contain:

    If / Else

logic.

---

## Triggers

A trigger is an action/event that starts a playbook.

Example:

    SIEM detects phishing alert
              ↓
        Playbook starts

### Easy Flow

    Trigger
       ↓
    Playbook
       ↓
    Automated Actions

---

# 5. Security Response

SOAR allows analysts to take actions using different security tools from:

    One Unified Interface

SOAR can also automate the response.

---

## Example — VPN Brute Force

A SOAR playbook can respond to a VPN brute-force incident by:

    VPN Brute Force Detected
             ↓
       Block IP on Firewall
             ↓
       Disable User in IAM
             ↓
       Open Ticket
             ↓
    Include Incident Details

This allows multiple response actions to happen through the SOAR workflow.

---

# 6. Threat Intelligence Management

Modern SOAR platforms can ingest:

    Threat Intelligence Feeds

SOAR can automatically compare internal alert data against these threat feeds.

### Purpose

This enriches the incident context immediately when the alert arrives.

### Easy Flow

    Internal Alert
          +
    Threat Intelligence
          ↓
    Context Enrichment
          ↓
    Better Investigation

---

# 7. Incident Response Case Management

If automation cannot completely resolve an incident:

    Incident
       ↓
     CASE

SOAR provides a centralized dashboard for the case.

It can contain:

- Full audit trail
- Actions already performed by automation
- Timelines
- Evidence lockers
- Files
- Hashes
- Collaboration tools

### Easy Understanding

The analyst can see:

    What happened?
    What did automation already do?
    What evidence exists?
    What still needs to be done?

---

# 8. Traditional SOC Challenges

Traditional SOC environments can create several problems.

---

## Alert Fatigue — "Needle in a Haystack"

### Challenge

A traditional SOC can receive:

    Millions of logs every day

from:

- SIEM
- EDR
- Firewalls

This creates a massive number of alerts.

A high percentage may be:

    False Positives

Analysts may spend hours:

- Clicking through repetitive alerts
- Investigating unnecessary alerts

This can cause:

- Analyst burnout
- Important IOCs being missed

### IOC

**IOC = Indicator of Compromise**

---

## SOAR Remedy

SOAR acts as a:

    High-Speed Filter

It can run alerts through automated playbooks to:

- Deduplicate
- Correlate
- Filter known benign noise

Result:

    Large Alert Volume
          ↓
       SOAR
          ↓
    Filter / Correlate
          ↓
    High-Fidelity Incidents
          ↓
    Human Analyst

Analysts can focus on incidents that actually require human investigation and intuition.

---

# 9. Tool Disparate Fragmentation

## "Swivel-Chair" Effect

### Challenge

To investigate one suspicious email, an analyst may need to open multiple systems.

For example:

    Email Gateway
         ↓
    Threat Intelligence Portal
         ↓
    Active Directory
         ↓
    EDR Console

The analyst constantly switches between different consoles.

This:

    Context Switching
          ↓
    Slows Response Time

---

## SOAR Remedy

SOAR provides:

    Orchestration

It connects different tools through:

    APIs

and provides:

    Single Pane of Glass

The analyst stays inside the SOAR platform.

SOAR reaches out to the connected security tools on the analyst's behalf.

### Easy Flow

    Email Gateway
         +
    Threat Intelligence
         +
    Active Directory
         +
    EDR
         ↓
        APIs
         ↓
        SOAR
         ↓
    Single Interface

---

# 10. Sluggish MTTD / MTTR

## Challenge

Manual triage takes time.

Examples of repetitive manual tasks:

- Copy-pasting IP addresses into lookup tools
- Opening tickets manually
- Waiting for email confirmations from users

These activities can stretch an incident lifecycle from:

    Minutes → Days

---

## SOAR Remedy

Automation executes repetitive tasks at:

    Machine Speed

The class gives an example:

    Manual work
       ↓
    45 minutes

    SOAR playbook
       ↓
    Less than 5 seconds

This can drastically reduce:

    MTTR

### Easy Understanding

    Manual Repetitive Work
            ↓
         Slow

    SOAR Automation
            ↓
         Fast
            ↓
       Lower MTTR

---

# 11. Traditional SOC vs SOAR-Enabled SOC

| Feature | Traditional SOC | SOAR-Enabled SOC |
|---|---|---|
| Triage Time | Minutes to Hours — Manual lookups | Seconds — Automated enrichment |
| Playbook Execution | Written in PDF documents — Static | Executed via Code/Workflows — Dynamic |
| Human Role | Data gatherer and button clicker | High-level decision maker & Threat Hunter |
| Tool Ecosystem | Siloed, disconnected consoles | Orchestrated, unified API mesh |

---

# 12. Phishing SOAR Playbook

The phishing response workflow contains five main stages:

    1. Trigger & Ingestion
             ↓
    2. Enrichment & Triage
             ↓
    3. Analysis & Correlation
             ↓
    4. Response & Mitigation
             ↓
    5. Post-Incident & Reporting

---

# 13. Stage 1 — Trigger & Ingestion

The playbook can be triggered by:

- SIEM alert
- Email
- User reporting

Once triggered:

    Playbook Activated

The alert data is parsed.

Information shown includes:

- URL
- Sender
- Recipient
- Attachment hashes

### Easy Flow

    SIEM / Email Alert
           OR
      User Reporting
            ↓
      Playbook Activated
            ↓
       Alert Data Parsing
            ↓
    URL / Sender / Recipient /
      Attachment Hashes

---

# 14. Stage 2 — Enrichment & Triage

The playbook performs several checks.

## Threat Intelligence Lookup

It checks:

    URL / IP Reputation

using:

    VirusTotal / Cyberint

---

## Active Directory

Checks:

    User Profile
    +
    VIP Status

---

## EDR

Performs:

    Endpoint Posture Check

---

## High-Fidelity Decision

The workflow asks:

    IS ALERT HIGH FIDELITY?

### YES

Continue toward analysis.

### NO

    False Positive Dismissal

---

# 15. Stage 3 — Analysis & Correlation

The workflow performs:

## Correlate IOCs Across Network

It checks indicators across the network.

### IOC

    Indicator of Compromise

---

## Analyze Attachment in Sandbox

The attachment is analyzed in:

    Sandbox

---

## Check Past Incident History

Previous incidents are checked.

Then the workflow asks:

    IS IT MALICIOUS?

### YES

Continue toward response and mitigation.

### NO

    Close Case as Benign

---

# 16. Stage 4 — Response & Mitigation

The workflow can use two response tracks.

---

## Full Auto Track

Used for:

    High Confidence

Actions include:

### Block URL on Firewall

    Malicious URL
         ↓
    Firewall
         ↓
    Block

### Update EDR Policies

The EDR policies are updated.

### Reset User Password

The user's password is reset.

---

## Semi-Auto Track

Used when:

    Human Review is Required

The SOC analyst reviews the requested mitigation steps.

The workflow can then:

- Execute mitigation steps
- Delete email enterprise-wide
- Isolate host via EDR

### Easy Flow

    Human Review
         ↓
    Execute Mitigation
         ↓
    Delete Malicious Email
         ↓
    Isolate Host

---

# 17. Stage 5 — Post-Incident & Reporting

After the incident response:

## Update Ticketing System

Example:

    ServiceNow

The ticketing system is updated.

---

## Generate Incident Report

An incident report is generated.

---

## Share Threat Intelligence

Relevant threat intelligence is shared.

---

## Close Case

After required actions are completed:

    Close Case

---

# 18. Complete Phishing SOAR Workflow

    TRIGGER & INGESTION
            ↓
    SIEM / EMAIL ALERT
            OR
       USER REPORTING
            ↓
      PLAYBOOK ACTIVATED
            ↓
      ALERT DATA PARSING
            ↓
    ENRICHMENT & TRIAGE
            ↓
    TI LOOKUP
    ACTIVE DIRECTORY
    EDR CHECK
            ↓
    IS ALERT HIGH FIDELITY?
        ↙           ↘
      NO             YES
      ↓               ↓
    FALSE       ANALYSIS &
    POSITIVE     CORRELATION
    DISMISSAL         ↓
                 CORRELATE IOCs
                 ANALYZE ATTACHMENT
                 CHECK HISTORY
                       ↓
                 IS IT MALICIOUS?
                   ↙       ↘
                 NO         YES
                 ↓           ↓
            CLOSE CASE    RESPONSE &
             AS BENIGN    MITIGATION
                             ↓
                    FULL AUTO / SEMI-AUTO
                             ↓
                    POST-INCIDENT
                    & REPORTING
                             ↓
                    UPDATE TICKET
                             ↓
                    INCIDENT REPORT
                             ↓
                    SHARE THREAT INTEL
                             ↓
                       CLOSE CASE

---

# 19. Easy SOAR Memory

Remember SOAR as:

    CONNECT
       ↓
    AUTOMATE
       ↓
    RESPOND

### Connect

SOAR connects:

- SIEM
- EDR
- Firewall
- IAM
- Other security tools

### Automate

Uses:

- Playbooks
- Workflows
- Triggers
- Conditional logic

### Respond

Can:

- Block IP/URL
- Disable users
- Reset passwords
- Isolate hosts
- Delete malicious emails
- Open/update tickets

---

# 20. SOC Without SOAR vs With SOAR

## Traditional SOC

    Many Alerts
         ↓
    Manual Lookups
         ↓
    Tool Switching
         ↓
    Manual Actions
         ↓
    Slow Response
         ↓
    Analyst Fatigue

## SOAR-Enabled SOC

    Alerts
      ↓
    Automated Enrichment
      ↓
    Correlation
      ↓
    Playbook
      ↓
    Automated Response
      ↓
    Analyst Handles Important Decisions

---
