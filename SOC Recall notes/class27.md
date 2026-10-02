# SOC Analyst L1 — Class 27
# Raju Recall Notes

## SIEM — Security Information & Event Management

---

# ⚡ 30-SECOND RECALL

**SIEM = Security Information & Event Management**

SIEM is the central system of a modern SOC.

    Logs from different sources
              ↓
            SIEM
              ↓
    Detection + Investigation

SIEM provides visibility across the:

    Entire Enterprise

It combines logs from:

- Networks
- Clouds
- Firewalls
- Applications

Main idea:

    COLLECT → PROCESS → STORE → NORMALIZE → DETECT → INVESTIGATE

---

# 🔥 MUST REMEMBER

## 1. SIEM Dashboard

### Threat Landscape

- Critical
- High
- Medium
- Low

### Top Attack Vectors

- Phishing
- Malware
- Credential Stuffing
- DDoS

### Incident Queue

Tracks:

- Incident ID
- Severity
- User/Host
- Status
- Assigned Analyst

### SOC Metrics Shown

**MTTA = Mean Time to Acknowledge**

Example:

    8 mins

**MTTR = Mean Time to Respond**

Example:

    4 hrs

### Ingestion Health

Sources:

- Cloud
- Firewall
- Endpoint
- Identity

Important terms:

- Ingestion Rate
- EPS = Events Per Second
- License Utilization

### Hunting / Entity Behavior

- Geo-IP anomalies
- Unusual logins
- At-risk users/hosts
- Threat hunting search

---

# 2. SIEM Architecture

Three main stages:

    Stage A → Collection
    Stage B → Heavy Parsing & Data Reduction
    Stage C → Indexing & Storage

---

# 3. Universal Forwarder

**UF = Universal Forwarder**

Runs on:

- Endpoints
- Servers
- Domain Controllers

Main configuration:

    inputs.conf

Example:

    WinEventLog://Security

It:

1. Reads logs
2. Wraps them in a lightweight framing protocol
3. Sends them onward

Important port:

    TCP 9997

### Memory

    Endpoint
       ↓
    Universal Forwarder
       ↓
    TCP 9997

---

# 4. Heavy Forwarder

**HF = Heavy Forwarder**

Used before long-term storage.

### Data Filtering

Uses Regex rules in:

    props.conf
    transforms.conf

Can remove:

- Routine firewall allowed logs
- Debug noise

Purpose:

    Less unnecessary data
          ↓
    Lower ingestion
          ↓
    Lower licensing cost

### Anonymization / Masking

Can mask:

- PII
- Social Security Numbers
- Credit card information

Uses:

    Regex

Example:

    XXXX-XX-1234

Related frameworks:

- GDPR
- PCI-DSS

---

# 5. Splunk Indexer

The Indexer converts:

    Raw Text
       ↓
    Structured + Searchable Data

### Parsing

It:

- Breaks data into events
- Extracts UTC timestamp
- Adds metadata

Important fields:

    _time
    host
    source
    sourcetype

### Easy Memory

    _time      → When?
    host       → Where from?
    source     → File/path
    sourcetype → Format

Examples of sourcetype:

    cisco:asa
    xmlwineventlog

---

# 6. Bucket Lifecycle

Data is stored in:

    Buckets

Order:

    HOT
      ↓
    WARM
      ↓
    COLD
      ↓
    FROZEN

### Hot

- Actively written
- Fast storage
- Searchable
- NVMe / SSD

### Warm

- Hot bucket rolled over
- Still searchable
- No new entries

### Cold

- Older data
- Cheap/high-capacity storage
- Mechanical or cloud object storage
- Search is slower

### Frozen

- Expired data
- Deleted, compressed, or archived
- Not searchable without manual re-indexing

---

# 7. Data Normalization — CIM

**CIM = Common Information Model**

Different vendors can use different names for the same thing.

Example:

    Palo Alto
    action=deny

    Zscaler
    block_type=policy_blocked

    AWS VPC
    log_status=REJECT

All can represent:

    Connection Blocked

### Problem

Without normalization, the analyst needs different queries for different vendors.

### Solution

CIM uses:

    Field Aliasing & Tagging

Vendor-specific fields are converted into standard fields.

Example:

    Action = "blocked"
    src_ip = "192.168.1.50"

### Important Query

    tag=network tag=communicate action=blocked src_ip=192.168.1.50

### Memory

    Different Vendors
          ↓
         CIM
          ↓
    Standard Fields
          ↓
    One Query

---

# 8. Real-Time Correlation

After logs are:

    Indexed + Normalized

SIEM becomes an:

    Active Real-Time Threat Detection Engine

It uses:

    Correlation Searches

inside:

    Splunk Enterprise Security (ES)

They run automatically.

Example:

    Every 5 minutes
          ↓
    Check previous 5 minutes

Language used:

    SPL
    Search Processing Language

---

# 9. Notable Event

When correlation conditions match:

    Correlation Search
          ↓
    Conditions Match
          ↓
    Notable Event
          ↓
    ES Triage Pane
          ↓
    SOC Analyst

---

# 10. Automatic Context Enrichment

SIEM extracts:

- User
- src_ip
- Host

Then checks:

    Internal Lookups / Watchlists

Example context:

- User = VP of Global Finance
- Host = contains PCI-compliant financial data

### Why Important?

The analyst gets additional context before investigating the alert.

---

# 11. SIEM vs EDR

| | SIEM | EDR |
|---|---|---|
| Scope | Global Enterprise | Localized Endpoint |
| SIEM/EDR Coverage | Cloud, Network, Identity, Applications, Endpoints | Laptops, Workstations, VM servers |
| Mechanism | Cross-log correlation + event aggregation | OS kernel behavioral inspection + memory tracking |
| Data | Structured/Unstructured logs | Native raw telemetry |

### SIEM Data Examples

- Syslog
- JSON
- API
- Event Channels

### EDR Data Examples

- Process creation
- File modification streams

### Easy Memory

    SIEM → Entire Enterprise

    EDR → Endpoint

---

# ⭐ INTERVIEW Q&A

## Q1. What is SIEM?

**Answer:**  
SIEM stands for Security Information & Event Management. It provides centralized security visibility across the enterprise.

## Q2. What are the three main SIEM processing stages?

**Answer:**

1. Collection
2. Heavy Parsing & Data Reduction
3. Indexing & Storage

## Q3. What is a Universal Forwarder?

**Answer:**  
It collects logs from endpoints, servers and domain controllers and forwards them to the next stage.

## Q4. What configuration is mainly used by the Universal Forwarder?

**Answer:**

    inputs.conf

## Q5. Which port is mentioned for the Universal Forwarder stream?

**Answer:**

    TCP 9997

## Q6. What is the purpose of a Heavy Forwarder?

**Answer:**  
It performs processing such as filtering and masking before data reaches long-term storage.

## Q7. What is CIM?

**Answer:**  
CIM stands for Common Information Model. It converts different vendor-specific fields into standard fields.

## Q8. What is a correlation search?

**Answer:**  
An automated search that checks logs for defined conditions and can generate a Notable Event.

## Q9. What is a Notable Event?

**Answer:**  
An event generated when the conditions of a correlation search are met.

## Q10. What is the difference between SIEM and EDR?

**Answer:**  
SIEM provides enterprise-wide visibility using cross-log correlation, while EDR focuses on endpoint activity using raw telemetry and behavioral inspection.

## Q11. What are the important SIEM metadata fields?

**Answer:**

    _time
    host
    source
    sourcetype

## Q12. What is the bucket lifecycle?

**Answer:**

    Hot → Warm → Cold → Frozen

## Q13. What is EPS?

**Answer:**  
EPS means Events Per Second.

## Q14. What is automatic context enrichment?

**Answer:**  
The SIEM extracts fields such as user, source IP and host and checks them against internal Lookups/Watchlists to add context.

## Q15. What is SPL?

**Answer:**  
SPL stands for Search Processing Language.

---

# 🧠 SOC ANALYST MINDSET

When working with SIEM, think:

    LOGS
      ↓
    COLLECT
      ↓
    PROCESS
      ↓
    INDEX
      ↓
    NORMALIZE
      ↓
    CORRELATE
      ↓
    ALERT
      ↓
    ENRICH
      ↓
    INVESTIGATE

### Remember

When an alert appears, useful context includes:

- User
- Source IP
- Host
- Severity
- Related logs
- Lookup / Watchlist information

### Core L1 Thinking

    What happened?
         ↓
    Where?
         ↓
    Who?
         ↓
    What other logs support it?
         ↓
    Investigate

---

# 📝 QUESTION PAPER MODE

1. What is SIEM?
2. What are the three SIEM processing stages?
3. What is a Universal Forwarder?
4. What is `inputs.conf`?
5. What is TCP 9997 used for?
6. What is a Heavy Forwarder?
7. Why is log filtering performed?
8. What is CIM?
9. Why is data normalization needed?
10. What is a correlation search?
11. What is a Notable Event?
12. What is the bucket lifecycle?
13. What is EPS?
14. What is automatic context enrichment?
15. What is the difference between SIEM and EDR?

---

# ✅ ANSWER KEY

1. Security Information & Event Management; centralized enterprise security visibility.
2. Collection → Heavy Parsing & Data Reduction → Indexing & Storage.
3. A log collection and forwarding component.
4. The main configuration mentioned for Universal Forwarder inputs.
5. The stream-shunting connection mentioned for forwarding logs.
6. An intermediate processing stage for filtering and masking.
7. To remove unnecessary logs and reduce ingestion/licensing load.
8. Common Information Model.
9. To convert different vendor-specific fields into standard fields.
10. An automated search that checks defined conditions.
11. An event generated when correlation conditions match.
12. Hot → Warm → Cold → Frozen.
13. Events Per Second.
14. Enriching events using fields such as user, src_ip and host with internal Lookups/Watchlists.
15. SIEM has enterprise-wide visibility; EDR focuses on endpoint visibility and raw endpoint telemetry.

---

# 🧩 FINAL MEMORY MAP

    SIEM
     │
     ├── COLLECTION
     │      └── Universal Forwarder
     │
     ├── PROCESSING
     │      └── Heavy Forwarder
     │           ├── Filtering
     │           └── Masking
     │
     ├── STORAGE
     │      └── Indexer
     │           └── Hot → Warm → Cold → Frozen
     │
     ├── NORMALIZATION
     │      └── CIM
     │
     ├── DETECTION
     │      └── Correlation Search
     │             ↓
     │        Notable Event
     │
     ├── ENRICHMENT
     │      └── Lookups / Watchlists
     │
     └── INVESTIGATION
            └── SOC Analyst

---

# 🔥 30-SECOND FINAL REVISION

**SIEM = Security Information & Event Management**

**UF = Universal Forwarder**

**HF = Heavy Forwarder**

**Indexer = Structures and stores searchable data**

**TCP 9997 = Universal Forwarder stream**

**CIM = Common Information Model**

**SPL = Search Processing Language**

**Correlation Search = Automated detection search**

**Notable Event = Matching correlation alert**

**Buckets = Hot → Warm → Cold → Frozen**

**EPS = Events Per Second**

**SIEM = Enterprise-wide visibility**

**EDR = Endpoint visibility**

---
