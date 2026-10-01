# SOC Analyst L1 — Class 25
# Raju Recall Notes

## SOC Workbooks, Lookups, Assets, Identities & SOC Metrics

---

# ⚡ 30-SECOND RECALL

### Workbook
**Workbook = VISUALIZE**

- Interactive, canvas-based report.
- Pulls data from logs.
- Shows data as:
  - Charts
  - Maps
  - Grids
- Updates when new logs arrive.
- Combines multiple data sources into one **Single Pane of Glass**.

### Lookup
**Lookup = ADD CONTEXT**

- Custom table uploaded to a security platform.
- In Sentinel, often called a **Watchlist**.
- Adds information that may be missing from raw logs.

### Asset
**Asset = WHAT?**

- Physical or virtual resource that:
  - Stores data
  - Processes data
  - Transmits data

### Identity
**Identity = WHO?**

- Digital representation of an entity that can perform actions.

### SOC Metrics
**Metrics = MEASURE SOC PERFORMANCE**

- Operational
- Efficiency
- Strategic

---

# 🔥 MUST REMEMBER

## 1. WORKBOOK

### Key Features

| Feature | Meaning |
|---|---|
| Real-Time Monitoring | Updates when new logs arrive |
| Interactivity | Click/filter data |
| Consolidation | Combines multiple sources |

### SOC Use Cases

- Incident Overview
- Threat Hunting
- Health Monitoring

### Memory

    Workbook
        ↓
    VISUALIZE

---

# 2. LOOKUPS

## Why?

Raw logs can be "thin".

Example:

    IP 192.168.1.5 accessed a file.

The log may not tell us:

- Who owns the IP?
- What device is it?
- Is it important?
- Is it a high-value server?

Lookup provides additional context.

## Types

| Lookup | Remember |
|---|---|
| Asset Inventory | IP → Hardware / Owner |
| Threat Intel | Malicious IPs / File Hashes |
| VIP List | Executives / Administrators |
| Terminated Users | Recently left employees |

### Sentinel

    Lookup = Watchlist

### KQL

Lookups can be used to:

- Filter data
- Join data

---

# 3. WORKBOOK + LOOKUP

    Lookup
       ↓
    Identifies VIP
       ↓
    SIEM detects unusual login
       ↓
    Alert
       ↓
    Workbook displays alert on global map
       ↓
    SOC sees geographic anomaly

---

# 4. ASSETS — "WHAT?"

## Definition

Asset = physical or virtual resource that:

- Stores data
- Processes data
- Transmits data

SOC tracks assets to understand:

    Blast Radius

## Categories

### Endpoints

- Laptops
- Workstations
- Mobile devices

### Infrastructure

- On-premises servers
- Cloud servers
- Virtual machines
- Containers

### Network Devices

- Routers
- Switches
- Firewalls
- Load balancers

### IoT / OT

- Smart cameras
- Printers
- Industrial Control Systems
- PLCs

## Asset Metadata

Remember:

    Criticality
    Ownership
    Patch Status

---

# 5. IDENTITIES — "WHO?"

## Types

### User Identity

- Employees
- Contractors
- Guests

### Privileged Identity

- Domain Admins
- Global Admins

### Service Principal / Non-Human Identity

Used by:

- Applications
- Scripts

### Managed Identity

Automatically managed by cloud providers such as:

- Azure
- AWS

Used for:

    Resource → Resource Communication

---

# 6. IDENTITY PERIMETER

### Remember

**"Identity is the new perimeter."**

Why?

- Users work from home.
- Users use cloud applications.
- Users are not always inside the physical office.

Security uses:

- MFA
- Conditional Access

---

# 7. ASSETS vs IDENTITIES

| | Assets | Identities |
|---|---|---|
| Focus | Hardware, Software & Infrastructure | Users, Groups & Service Accounts |
| Goal | Vulnerability Management & Patching | Access Control & Behavior Monitoring |
| Risk | Device compromised/unpatched? | Account stolen/misused? |
| Security Tool | EDR | IAM |

### Easy Memory

    Asset    → WHAT?
    Identity → WHO?

---

# 8. SOC METRICS

## Definition

Metrics are:

**Quantifiable data points used to measure success.**

They are described as the:

**"Heartbeat of the operation."**

### Objective vs Metric

    Objective
       ↓
    What you want to achieve

    Metric
       ↓
    How you measure success

---

# 9. THREE SOC METRIC CATEGORIES

    SOC Metrics
        │
        ├── Operational
        ├── Efficiency
        └── Strategic

---

# 10. THE "BIG THREE"

## MTTA

**Mean Time to Acknowledge**

    Alert fires
       ↓
    Analyst assigns it
       ↓
    Analyst starts looking

### Remember

    MTTA = ACKNOWLEDGE

### High MTTA

Can indicate:

- Too many alerts
- Alert fatigue
- Not enough staff

---

## MTTR

**Mean Time to Respond / Remediate**

Measures the average time needed to:

    Close an incident
          ↓
    Neutralize the threat

### Remember

    MTTR = RESPOND / REMEDIATE

---

## MTTD

**Mean Time to Detect**

Measures how long a threat exists before security tools trigger an alert.

Tools:

- SIEM
- EDR
- IDS

### Remember

    MTTD = DETECT

### Goal

    Lower MTTD
        =
    Detect faster

### Example

    Hacker enters Monday
          ↓
    SIEM alerts Thursday
          ↓
    MTTD = 3 days

---

# 11. IMPROVING MTTD

### Better Log Coverage

**You can't detect what you can't see.**

    Better Visibility
          ↓
    Better Detection

### Advanced Analytics

Move beyond:

    If / Then

Use:

    Machine Learning (ML)

### Threat Intelligence

Use Lookups to flag known bad indicators.

---

# 12. EFFICIENCY & QUALITY METRICS

## False Positive Rate

Percentage of alerts that are:

    Noise / Benign Activity

### High False Positives

    Too Much Noise
          ↓
    Analysts Stop Paying Attention
          ↓
    Alert Fatigue

---

## True Positive Rate

Percentage of alerts that are:

    Actual Security Incidents

---

## Alert Volume vs Incident Volume

Compares:

    Raw Alerts
        vs
    Actual Security Incidents

Example:

    10,000 Alerts
         ↓
      2 Incidents

---

# 13. STRATEGIC & RISK METRICS

Three important metrics:

- Dwell Time
- Coverage Mapping
- SLA Compliance

### Dwell Time

    Initial Infection
          ↓
    SOC Detection

    Dwell Time = Detection Time - Infection Time

### Coverage Mapping

Measures how much of the:

    "Attacker Playbook"

the organization can see.

Example:

    80% Coverage
    for Ransomware Techniques

### SLA Compliance

Percentage of critical incidents handled within the promised timeframe.

Example:

    95% of Critical Alerts
    acknowledged within 15 minutes

---

# 14. METRIC BREAKDOWN

| Metric | High Value | Low Value |
|---|---|---|
| MTTA | Understaffed / Alert fatigue | Responsive team |
| MTTR | Complex / Slow processes | Effective automation |
| False Positive % | "Crying Wolf" / Bad rules | High-fidelity alerts |
| Dwell Time | "Silent" breach | Rapid detection |

### Memory

    High MTTA
      → Understaffing / Alert Fatigue

    High MTTR
      → Complex / Slow Processes

    High False Positive %
      → Bad Rules / "Crying Wolf"

    High Dwell Time
      → Silent Breach

---

# 15. WHY METRICS MATTER

Metrics should drive:

    ACTION

### High MTTA

- Buy an automation tool such as SOAR.
- Hire a Tier 1 analyst.

### High False Positives

- Tune KQL queries.
- Tune Lookups.

### High MTTR

- Build better Workbooks.
- Put required data in one place.
- Reduce manual searching by analysts.

---

# 16. VANITY METRICS

A metric may look impressive but may not show meaningful security performance.

### Example

    "We blocked 1 million hits!"

Many may simply be:

- Random internet scans
- Activity that does not actually pose a risk

### Remember

Focus on metrics that show the SOC is:

    FAST + ACCURATE

---

# ⭐ INTERVIEW Q&A

## Q1. What is a SOC Workbook?

**Answer:**  
An interactive, canvas-based report that visualizes security data using charts, maps and grids.

## Q2. What are the three key Workbook features?

**Answer:**

- Real-Time Monitoring
- Interactivity
- Consolidation

## Q3. What is a Lookup?

**Answer:**  
A custom table that provides additional context to security data.

## Q4. What is a Lookup called in Sentinel?

**Answer:**  
Watchlist.

## Q5. What are the four Lookup types discussed?

**Answer:**

- Asset Inventory
- Threat Intel
- VIP List
- Terminated Users

## Q6. What is an Asset and what is an Identity?

**Answer:**

    Asset    → WHAT?
    Identity → WHO?

## Q7. What are the three core operational metrics?

**Answer:**

- MTTA
- MTTR
- MTTD

## Q8. What is the difference between MTTA, MTTD and MTTR?

**Answer:**

    MTTA → Acknowledge
    MTTD → Detect
    MTTR → Respond / Remediate

## Q9. What is Dwell Time?

**Answer:**  
The time between initial infection and SOC detection.

    Dwell Time = Detection Time - Infection Time

## Q10. What is a False Positive?

**Answer:**  
An alert that turns out to be benign/noise.

## Q11. What is a True Positive?

**Answer:**  
An alert that represents an actual security incident.

## Q12. What is Coverage Mapping?

**Answer:**  
It measures how much of the attacker's playbook the organization can actually see.

## Q13. What is SLA Compliance?

**Answer:**  
The percentage of critical incidents handled within the promised timeframe.

## Q14. What is a Vanity Metric?

**Answer:**  
A metric that may look impressive but does not necessarily demonstrate meaningful security performance.

## Q15. What is the main difference between Assets and Identities?

**Answer:**

    Asset    → WHAT?
    Identity → WHO?

---

# 🧠 SOC ANALYST MINDSET

When looking at security data:

    Raw Logs
       ↓
    Lookup / Enrichment
       ↓
    SIEM Detection
       ↓
    Workbook Visualization
       ↓
    Analyst Investigation
       ↓
    Metrics
       ↓
    Action

### Remember

- **Workbook** → Visualize
- **Lookup** → Add Context
- **Asset** → What?
- **Identity** → Who?
- **Metrics** → How is the SOC performing?

---

# 📝 QUESTION PAPER MODE

## Try answering without looking above.

1. What is a Workbook?
2. What are the three key Workbook features?
3. What is a Lookup and why is it useful?
4. Name the four Lookup types.
5. What is the difference between an Asset and an Identity?
6. What are the four asset categories?
7. What are the main types of identities?
8. What are MTTA, MTTD and MTTR?
9. What is the difference between False Positive and True Positive?
10. What is Dwell Time?
11. What is Coverage Mapping?
12. What is SLA Compliance?
13. What can high MTTA indicate?
14. What can high False Positive Rate indicate?
15. What is a Vanity Metric?

---

# ✅ ANSWER KEY

1. An interactive, canvas-based report used to visualize security data.
2. Real-Time Monitoring, Interactivity and Consolidation.
3. A Lookup is a custom table that adds context to security data; it helps because raw logs may not contain enough information.
4. Asset Inventory, Threat Intel, VIP List and Terminated Users.
5. Asset = WHAT resource is involved; Identity = WHO/WHAT entity is performing the action.
6. Endpoints, Infrastructure, Network Devices and IoT/OT.
7. User Identities, Privileged Identities, Service Principals/Non-Human Identities and Managed Identities.
8. MTTA = Acknowledge, MTTD = Detect, MTTR = Respond/Remediate.
9. False Positive = benign/noise; True Positive = actual security incident.
10. Time between initial infection and SOC detection.
11. Measurement of how much of the attacker's playbook the organization can see.
12. Percentage of critical incidents handled within the promised timeframe.
13. Too many alerts, alert fatigue or insufficient staff.
14. "Crying Wolf", bad detection rules and alert fatigue.
15. A metric that looks impressive but may not demonstrate meaningful security performance.

---

# 🧩 FINAL MEMORY MAP

    SOC
     │
     ├── WORKBOOK
     │      ↓
     │   VISUALIZE
     │
     ├── LOOKUP
     │      ↓
     │   ADD CONTEXT
     │
     ├── ASSET
     │      ↓
     │   WHAT?
     │
     ├── IDENTITY
     │      ↓
     │   WHO?
     │
     └── METRICS
            │
            ├── MTTA → Acknowledge
            ├── MTTD → Detect
            ├── MTTR → Respond / Remediate
            ├── False Positive → Noise
            ├── True Positive → Real Incident
            ├── Dwell Time → Infection → Detection
            ├── MITRE Coverage → Attacker Playbook Visibility
            └── SLA → Promised Timeframe

---

# 🔥 ONE-MINUTE FINAL REVISION

**Workbook = VISUALIZE**

**Lookup = ADD CONTEXT**

**Asset = WHAT**

**Identity = WHO**

**MTTA = ACKNOWLEDGE**

**MTTD = DETECT**

**MTTR = RESPOND / REMEDIATE**

**False Positive = BENIGN**

**True Positive = REAL INCIDENT**

**Dwell Time = INFECTION → DETECTION**

**MITRE Coverage = ATTACKER PLAYBOOK VISIBILITY**

**SLA = PROMISED TIMEFRAME**

**Vanity Metric = Impressive number that may not show real security performance**

---
