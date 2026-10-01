# SOC Analyst L1 — Class 25

## Topic: SOC Workbooks, Lookups, Assets, Identities & SOC Metrics

### Training

- By Nitesh Singh
- Job Ready Free Live Training To Become A SOC Analyst L1 For Free
- Defronix Cyber Security

---

# 1. SOC Workbooks — The Visualization Engine

## What is a Workbook?

A **Workbook** is an interactive, canvas-based report.

It:

- Pulls data from different logs.
- Takes raw text/data.
- Converts that data into:
  - Charts
  - Maps
  - Grids

### Easy Understanding

A Workbook helps a SOC analyst **see security data visually** instead of looking only at raw logs.

---

# 2. Key Features of Workbooks

## 2.1 Real-Time Monitoring

A static PDF does not automatically change when new data arrives.

A Workbook is different:

- New logs arrive.
- The Workbook updates.
- The SOC can see new security activity.

### Easy Meaning

    New Logs
       ↓
    Workbook Updates
       ↓
    SOC Sees New Activity

---

## 2.2 Interactivity

A Workbook is interactive.

The analyst can click on data shown in the Workbook.

### Example

Suppose a bar chart shows:

    Failed Login

There is a spike in failed logins.

The analyst clicks that spike.

The Workbook can automatically filter the rest of the page and show only those specific events.

### Easy Meaning

    Click suspicious data
            ↓
    Workbook filters related events
            ↓
    Analyst investigates

---

## 2.3 Consolidation

A Workbook can combine data from different sources into one place.

### Example Sources

- Firewall logs
- Office 365
- Endpoint data

All of these can be brought into one view.

This is called:

    Single Pane of Glass

### Easy Meaning

Instead of checking every source separately:

    Firewall
       +
    Office 365
       +
    Endpoint
       ↓
    One Workbook

---

# 3. Workbook Use Cases in the SOC

## 3.1 Incident Overview

A dashboard can show:

- How many "High" severity alerts are currently open.
- Who is assigned to those alerts.

### Purpose

The SOC can quickly understand the current incident situation.

---

## 3.2 Threat Hunting

Workbooks can visualize:

- Network traffic patterns
- Beaconing behavior

This helps the analyst spot suspicious communication patterns.

---

## 3.3 Health Monitoring

Workbooks can be used to check whether:

- Servers are successfully sending logs to the SIEM.

### Easy Meaning

    Servers
       ↓
    Send Logs
       ↓
    SIEM

The Workbook helps monitor whether this logging is working properly.

---

# 4. SOC Lookups — The Enrichment Tool

## What is a Lookup?

A **Lookup** is a custom table of data uploaded to a security platform.

It provides additional context that may not be available in standard logs.

### Sentinel

A Lookup is often called a:

    Watchlist

in Sentinel.

---

# 5. Why Do We Need Lookups?

Raw logs are often:

    "Thin"

This means the log may contain some information but not enough context.

### Example

A log may tell us:

    IP 192.168.1.5 accessed a file.

But the log may not tell us:

- Who owns this IP?
- What device is using this IP?
- Is this device important?
- Is this a high-value server?

The Lookup helps bridge this gap.

### Easy Understanding

    Raw Log
       ↓
    Limited information
       ↓
    Lookup
       ↓
    Additional context

---

# 6. Common Types of Lookups

| Type | Description | Example Data |
|---|---|---|
| Asset Inventory | Maps IPs to specific hardware or owners | `10.0.0.5 = HR_Database_Server` |
| Threat Intel | List of known malicious IPs or file hashes | `8.8.8.8 = Known_Malware_Source` |
| VIP List | Tracks high-profile users such as Executives/Admins | `jdoe@company.com = CFO` |
| Terminated Users | List of employees who recently left | Helps spot "ghost" account logins |

---

# 7. Asset Inventory Lookup

## Purpose

Asset Inventory maps:

    IP Address
       ↓
    Specific Hardware / Owner

### Example

    10.0.0.5 = HR_Database_Server

This tells the SOC analyst what hardware or asset is associated with the IP.

---

# 8. Threat Intel Lookup

## Purpose

A Threat Intel Lookup contains a list of known:

- Malicious IP addresses
- Malicious file hashes

### Example

    8.8.8.8 = Known_Malware_Source

This provides information about known malicious indicators.

---

# 9. VIP List Lookup

## Purpose

A VIP List tracks high-profile users.

Examples:

- Executives
- Administrators

### Example

    jdoe@company.com = CFO

This tells the SOC that the account belongs to a high-profile user.

---

# 10. Terminated Users Lookup

## Purpose

This Lookup contains employees who recently left the organization.

### SOC Use

It can help identify:

    "Ghost" account logins

### Easy Example

An employee leaves the company.

Their account should no longer be actively used.

If that account is still being used, the Terminated Users Lookup can help the SOC identify the login.

---

# 11. How Lookup Works in a Query

When a SOC analyst writes a query such as:

    KQL

they can use the Lookup to:

- Filter data
- Join data

### Example Logic

Show all logins where the username is found in:

    Terminated_Users

Lookup table.

### Easy Meaning

    Login Data
        +
    Terminated_Users Lookup
        ↓
    Find logins involving terminated users

---

# 12. How Workbooks and Lookups Work Together

Imagine the SOC is investigating a suspicious login.

## Step 1 — Lookup

The Lookup tells the system that the user is:

    VIP

For example:

    CFO

---

## Step 2 — SIEM Alert

The SIEM detects that:

- The CFO is logging in.
- The login is coming from an unusual country.

This triggers an alert.

---

## Step 3 — Workbook

The Workbook displays the alert:

- On a global map
- Highlighted in red

This allows the SOC Manager to quickly see the geographic anomaly.

### Complete Flow

    Lookup
       ↓
    Identifies VIP
       ↓
    SIEM detects unusual login
       ↓
    Alert triggered
       ↓
    Workbook displays alert on global map
       ↓
    SOC Manager sees geographic anomaly

---

# 13. Assets — The "What"

## What is an Asset?

An **asset** is any physical or virtual resource that:

- Stores data
- Processes data
- Transmits data

---

## Why Does a SOC Track Assets?

The SOC tracks assets to understand the:

    "Blast Radius"

of an attack.

### Easy Meaning

The SOC wants to know:

> If an attack happens, which systems/resources could be affected?

---

# 14. Categories of Assets

## 14.1 Endpoints

Examples:

- Laptops
- Workstations
- Mobile devices

These are used by employees.

---

## 14.2 Infrastructure

Examples:

- On-premises servers
- Cloud servers
- Virtual machines
- Containers

---

## 14.3 Network Devices

Examples:

- Routers
- Switches
- Firewalls
- Load balancers

---

## 14.4 IoT / OT

Examples:

- Smart cameras
- Printers
- Industrial Control Systems
- PLCs

---

# 15. Asset Context — Metadata

Knowing that a device exists is not enough.

A SOC analyst also needs additional information about the asset.

---

## 15.1 Criticality

The analyst needs to know how important the asset is.

### Example

    Test Machine
         vs
    Production Database

The production database may represent a much more important asset.

---

## 15.2 Ownership

The analyst should know:

- Who is the primary user?
- Who is the system administrator?

---

## 15.3 Patch Status

The analyst should know:

- Is the system patched?
- Is it running an outdated operating system?
- Does it have known vulnerabilities?

---

# 16. Identities — The "Who"

## What is an Identity?

An **identity** is a digital representation of an entity that can perform actions.

It is no longer only about a human person.

Anything that has a set of permissions can be an identity.

### Easy Meaning

Identity answers:

    "WHO or WHAT is performing an action?"

---

# 17. Types of Identities

## 17.1 User Identities

These represent human users.

Examples:

- Employees
- Contractors
- Guests

---

## 17.2 Privileged Identities

These are administrator accounts with high-level privileges.

Examples:

- Domain Admins
- Global Admins

These accounts have very high access.

---

## 17.3 Service Principals / Non-Human Identities

These are accounts used by:

- Applications
- Scripts

They allow applications or scripts to communicate with other systems.

### Example

A backup script needs access to a database.

The identity used by that script is a:

    Non-Human Identity

---

## 17.4 Managed Identities

Managed Identities are identities automatically managed by cloud providers.

Examples mentioned:

- Azure
- AWS

They are used for:

    Resource-to-Resource Communication

---

# 18. The Identity Perimeter

In modern security, the concept is:

    "Identity is the new perimeter."

## Why?

People:

- Work from home.
- Use cloud applications.
- Are not always inside the physical office.

Therefore, the physical office boundary is no longer enough.

Security now depends on verifying identity through:

- MFA
- Conditional Access

---

# 19. Assets vs Identities

| Feature | Assets | Identities |
|---|---|---|
| Focus | Hardware, Software & Infrastructure | Users, Groups & Service Accounts |
| Goal | Vulnerability Management & Patching | Access Control & Behavior Monitoring |
| Risk | Is the device compromised or unpatched? | Is the account stolen or misused? |
| Security Tool | EDR (Endpoint Detection & Response) | IAM (Identity & Access Management) |

---

# 20. Understanding Assets vs Identities

## Assets

Assets focus on:

- Hardware
- Software
- Infrastructure

### Main Goal

    Vulnerability Management & Patching

### Main Risk Question

    Is the device compromised or unpatched?

### Security Tool

    EDR
    Endpoint Detection & Response

---

## Identities

Identities focus on:

- Users
- Groups
- Service Accounts

### Main Goal

    Access Control & Behavior Monitoring

### Main Risk Question

    Is the account stolen or misused?

### Security Tool

    IAM
    Identity & Access Management

---

# 21. SOC Metrics

## What are SOC Metrics?

In a SOC, metrics are described as:

    "The heartbeat of the operation."

They tell you whether the SOC team is:

- Working effectively
- Dealing with too much noise

---

## Objective vs Metric

### Objective

An objective defines:

    What you want to achieve.

### Example

    Reduce the risk of data breaches.

---

### Metric

A metric is a:

    Quantifiable data point

used to measure success.

### Easy Understanding

    Objective
       ↓
    What do we want?
       ↓
    Metric
       ↓
    How do we measure success?

---

# 22. Three SOC Metric Categories

SOC metrics are generally divided into three categories:

1. Operational
2. Efficiency
3. Strategic

---

# 23. Core Operational Metrics — The "Big Three"

The three core operational metrics are:

- MTTA
- MTTR
- MTTD

They measure how quickly the SOC team reacts to threats.

---

# 24. MTTA — Mean Time to Acknowledge

## What is MTTA?

MTTA is the average time from:

    Alert Fires
         ↓
    Analyst Assigns It to Themselves
         ↓
    Analyst Starts Looking at It

### Easy Meaning

    MTTA = How quickly an analyst acknowledges and starts investigating an alert.

---

## Why Does MTTA Matter?

High MTTA can mean:

- Too many alerts
- Alert fatigue
- Not enough staff

---

# 25. MTTR — Mean Time to Respond / Remediate

## What is MTTR?

MTTR is the average time it takes to:

    "Close" an incident

by neutralizing the threat.

### Easy Meaning

    MTTR = How long it takes to deal with and close the incident.

---

## Why Does MTTR Matter?

The longer a hacker remains inside a system:

    Longer hacker presence
           ↓
    More potential damage

The class connects this attacker presence with:

    Dwell Time

---

# 26. MTTD — Mean Time to Detect

## What is MTTD?

MTTD measures how long a threat exists in the environment before security tools actually trigger an alert.

### Security Tools Mentioned

- SIEM
- EDR
- IDS

---

## MTTD Goal

The goal is:

    Lower MTTD

Meaning:

    Detect threats faster.

---

# 27. MTTD Example

Suppose:

- A hacker entered the network on Monday.
- The SIEM did not alert until Thursday.

Then:

    MTTD = 3 days

---

# 28. Why MTTD Is Tricky

Sometimes the SOC does not know exactly when the:

    "Actual Incident"

started.

The actual start time may only become known after the investigation is completed.

---

# 29. How to Improve MTTD

## 29.1 Better Log Coverage

The class states:

    "You can't detect what you can't see."

Therefore:

- Better log coverage
- Better visibility
- Better detection

---

## 29.2 Advanced Analytics

Move beyond simple:

    If / Then

rules.

Use:

    ML
    Machine Learning

to identify anomalies.

### Example

A user suddenly logs in from a new country.

ML-based analytics can help identify this unusual behavior.

---

## 29.3 Threat Intelligence

Use Lookups to automatically flag known bad indicators.

### Example

A known malicious IP touches the network.

A Lookup can automatically help flag it.

---

# 30. Efficiency & Quality Metrics

These metrics help determine whether:

- Tools are working.
- Processes are working.

The class covers:

1. False Positive Rate
2. True Positive Rate
3. Alert Volume vs Incident Volume

---

# 31. False Positive Rate

## Meaning

False Positive Rate is the percentage of alerts that turn out to be:

    "Noise"

or:

    Benign Activity

---

## Goal

Keep the False Positive Rate low.

### Example from the Class

If:

    90% of alerts = False Positives

analysts may stop paying attention.

This can create alert fatigue.

---

# 32. True Positive Rate

## Meaning

True Positive Rate is the percentage of alerts that are:

    Actual Security Incidents

This helps validate whether detection rules are:

    "Tuned"

correctly.

---

# 33. Alert Volume vs Incident Volume

This compares:

    Raw "Pings"
          vs
    Actual "Problems"

### Example

    10,000 Alerts
          ↓
       2 Incidents

This indicates the SIEM needs better filtering.

---

# 34. Strategic & Risk Metrics

These metrics are shown to the:

- CISO
- CEO
- C-Suite

They help justify the SOC budget.

The class covers:

1. Dwell Time
2. Coverage Mapping
3. SLA Compliance

---

# 35. Dwell Time

## Meaning

Dwell Time is the time between:

    Initial Infection
          ↓
    SOC Finally Detects It

### Formula

    Dwell Time = Detection Time - Infection Time

---

# 36. Coverage Mapping — MITRE ATT&CK

Coverage Mapping shows how much of the:

    "Attacker Playbook"

the organization can actually see.

### Example

    80% Coverage for Ransomware Techniques

This represents how much of the relevant attacker techniques the organization can see/detect.

---

# 37. SLA Compliance

## SLA

    Service Level Agreement

## SLA Compliance

It is the percentage of:

    "Critical" incidents

handled within the promised timeframe.

### Example

    95% of Critical Alerts
    acknowledged within 15 minutes

---

# 38. Metric Breakdown

| Metric | Category | High Value = ? | Low Value = ? |
|---|---|---|---|
| MTTA | Speed | Bad: Understaffed / Alert fatigue | Good: Responsive team |
| MTTR | Impact | Bad: Complex / Slow processes | Good: Effective automation |
| False Positive % | Tuning | Bad: "Crying Wolf" / Bad rules | Good: High-fidelity alerts |
| Dwell Time | Visibility | Bad: "Silent" breach occurring | Good: Rapid detection |

---

# 39. MTTA — Metric Breakdown

## High MTTA

Can indicate:

- Understaffing
- Alert fatigue

## Low MTTA

Can indicate:

- Responsive team

---

# 40. MTTR — Metric Breakdown

## High MTTR

Can indicate:

- Complex processes
- Slow processes

## Low MTTR

Can indicate:

- Effective automation

---

# 41. False Positive Percentage — Metric Breakdown

## High False Positive %

Can indicate:

- "Crying Wolf"
- Bad detection rules

## Low False Positive %

Can indicate:

- High-fidelity alerts

---

# 42. Dwell Time — Metric Breakdown

## High Dwell Time

Can indicate:

    "Silent" breach occurring

## Low Dwell Time

Can indicate:

    Rapid detection

---

# 43. Why Metrics Matter

Metrics should not simply be numbers on a slide.

They should drive:

    Action

---

# 44. Action When MTTA Is High

If MTTA is high:

- Buy an automation tool such as SOAR.
- Hire a Tier 1 analyst.

---

# 45. Action When False Positives Are High

If False Positives are high:

- Spend a week tuning KQL queries.
- Tune Lookups.

---

# 46. Action When MTTR Is High

If MTTR is high:

- Build better Workbooks.
- Put all the required data in one place.
- Reduce the need for analysts to search for the required information.

---

# 47. Vanity Metrics

## What Are Vanity Metrics?

Vanity Metrics are metrics that may look impressive but do not necessarily show meaningful security performance.

### Example

    "We blocked 1 million hits!"

This may look impressive.

But many of those hits may simply be:

- Random internet scans
- Activity that does not actually pose a risk

---

# 48. What Should the SOC Focus On?

Instead of focusing on vanity metrics, focus on metrics that prove the team is:

- Fast
- Accurate

### Easy Meaning

The important question is not:

    "How big is the number?"

The important question is:

    "Does the metric show that the SOC is detecting and responding effectively?"

---

# 49. Complete Concept Flow

The class connects the topics as follows:

    Logs
      ↓
    Lookup
      ↓
    Additional Context
      ↓
    SIEM Detection
      ↓
    Workbook Visualization
      ↓
    SOC Investigation
      ↓
    Metrics
      ↓
    Action / Improvement

---

# 50. Easy Final Understanding

## Workbook

    VISUALIZE

Takes security data and shows it through:

- Charts
- Maps
- Grids

---

## Lookup

    ADD CONTEXT

Adds information that may not be present in raw logs.

---

## Asset

    "WHAT?"

Identifies the physical or virtual resource involved.

---

## Identity

    "WHO?"

Identifies the entity performing actions.

---

## MTTA

    ACKNOWLEDGE

How quickly the analyst starts looking at an alert.

---

## MTTD

    DETECT

How long a threat exists before a security tool alerts.

---

## MTTR

    RESPOND / REMEDIATE

How long it takes to close an incident by neutralizing the threat.

---

## Dwell Time

    INFECTION → DETECTION

Time between initial infection and SOC detection.

---

## False Positive

    ALERT → BENIGN

The alert turns out to be harmless/noise.

---

## True Positive

    ALERT → REAL SECURITY INCIDENT

The alert represents an actual security incident.

---

## MITRE ATT&CK Coverage

    HOW MUCH OF THE ATTACKER PLAYBOOK CAN WE SEE?

---

## SLA Compliance

    WERE CRITICAL INCIDENTS HANDLED WITHIN THE PROMISED TIME?

---
