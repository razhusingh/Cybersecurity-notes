# SOC Analyst L1 — Class 27
# Raju Full Notes

## SIEM — Security Information & Event Management System

---

# 1. SIEM

## What is SIEM?

**SIEM = Security Information & Event Management**

SIEM is the:

- Core operating system of a modern SOC
- Brain of the SOC
- Large data lake for security data

It is designed for:

- Real-time streaming analytics
- Long-term security retention
- Forensic compliance

### Easy Understanding

If EDR gives visibility into endpoints, SIEM gives visibility into the:

    Entire Enterprise

SIEM combines logs from:

- Networks
- Clouds
- Firewalls
- Applications

into one:

    Single Pane of Glass

---

# 2. SOC Operational SIEM Dashboard

The SOC dashboard provides an enterprise-wide view of security operations.

## Threat Landscape Overview

### Global Alert Severity

The dashboard displays alerts according to severity:

- Critical
- High
- Medium
- Low

### Top Attack Vectors

The dashboard tracks:

- Phishing
- Malware
- Credential Stuffing
- DDoS

### Alert Volume

Shows:

    Alert Volume — Last 24 Hours

This helps the SOC see how alert activity changes over time.

---

# 3. Incident Queue & Investigation

The incident queue provides information such as:

- Incident ID
- Severity
- User/Host
- Status
- Assigned Analyst

Example statuses include:

- Triage
- In Progress
- Contained

## MTTA

**Mean Time to Acknowledge**

Dashboard example:

    8 mins
    ON TRACK

## MTTR

**Mean Time to Respond**

Dashboard example:

    4 hrs
    NEEDS ATTENTION

---

# 4. Data Sources & Ingestion Health

The dashboard monitors the:

    Log Ingestion Pipeline

## Data Sources

The sources shown are:

- Cloud
- Firewall
- Endpoint
- Identity

### Ingestion Flow

    SYSLOG / AGENT
          ↓
    PARSING &
    CORRELATION
          ↓
    INDEXING TIER

## Ingestion Rate

The dashboard displays:

    Ingestion Rate by Source
    GB / DAY

## EPS

**EPS = Events Per Second**

The dashboard also monitors:

    License Utilization

---

# 5. Entity Behavior & Hunting

The dashboard provides visibility into:

## Geo-IP Anomalies

Shows unusual geographic activity.

## Unusual Logins

Helps identify unusual login behavior.

## Top At-Risk Entities

Shows risk information for:

- Users
- Hosts

## Threat Hunting Search

Provides a search area for:

    Threat Hunting

---

# 6. SIEM Ingestion & Processing Pipeline

SIEM is a large system that:

- Ingests unstructured or semi-structured data
- Normalizes the data
- Optimizes it for fast text searching

The processing pipeline has three main stages:

    Stage A → Collection
    Stage B → Heavy Parsing & Data Reduction
    Stage C → Indexing & Storage

---

# 7. Stage A — Collection

## Universal Forwarders

Logs originate at the edge of the network.

Splunk uses:

    Universal Forwarders (UFs)

Universal Forwarders are optimized C++ binaries that run on:

- Endpoints
- Servers
- Domain Controllers

They are designed to have almost zero CPU overhead on the systems where they run.

---

# 8. Universal Forwarder Mechanism

The Universal Forwarder uses configuration templates.

The main configuration mentioned is:

    inputs.conf

It monitors:

- Specific directories
- Event channels

### Example

    WinEventLog://Security

The Universal Forwarder:

1. Reads the log line.
2. Wraps it in a lightweight framing protocol.
3. Sends it to the next stage.

The stream is sent through:

    TCP Port 9997

### Easy Flow

    Endpoint / Server / Domain Controller
                    ↓
          Universal Forwarder
                    ↓
                Read Logs
                    ↓
              TCP Port 9997
                    ↓
              Next Stage

---

# 9. Stage B — Heavy Parsing & Data Reduction

Before data reaches long-term storage, it passes through:

    Heavy Forwarder (HF)

or an:

    Intermediate Tier

This stage is important for:

- SOC performance
- Financial/budget considerations

---

# 10. Data Filtering

SOC engineers can use:

    Regex Rules

inside:

    props.conf
    transforms.conf

These rules can remove unnecessary logs before they reach the indexer.

### Examples of Unnecessary Data

- Routine firewall "allowed" connection logs
- Debug noise

### Why Filter?

    Millions of Junk Logs
            ↓
       Filter Them
            ↓
      Less Ingestion
            ↓
    Lower Licensing Costs

---

# 11. Anonymization & Masking

Logs may contain:

    PII
    Personally Identifiable Information

Examples include:

- Cleartext Social Security Numbers
- Credit card information

The Heavy Forwarder can intercept this information and use:

    Regex

to mask it.

### Example

    XXXX-XX-1234

This helps comply with:

- GDPR
- PCI-DSS

### Easy Flow

    Sensitive PII
         ↓
    Heavy Forwarder
         ↓
       Regex
         ↓
    Mask Information
         ↓
    Privacy Compliance

---

# 12. Stage C — Indexing & Storage

## Splunk Indexer

The Splunk Indexer transforms:

    Raw Text Streams
          ↓
    Structured, Searchable Data

This is where heavy computational processing takes place.

---

# 13. Parsing Phase

The indexer:

1. Breaks the incoming text stream into discrete events.
2. Extracts the explicit UTC timestamp.
3. Adds core metadata.

## `_time`

Represents the explicit UTC timestamp.

## `host`

Shows:

    Where the data came from

## `source`

Shows:

    File Pathway

## `sourcetype`

Shows:

    Structural Format of the Data

Examples:

    cisco:asa
    xmlwineventlog

### Easy Memory

    _time
      → When?

    host
      → Where from?

    source
      → Which file/path?

    sourcetype
      → What format?

---

# 14. Bucket Lifecycle

Data is stored in time-series directories called:

    Buckets

There are four stages:

    Hot
      ↓
    Warm
      ↓
    Cold
      ↓
    Frozen

---

# 15. Hot Buckets

Hot buckets are:

- Actively being written to
- Stored on very fast storage
- Searchable

Storage mentioned:

- NVMe
- SSD

### Memory

    HOT
     ↓
    Active
     ↓
    Fast
     ↓
    Searchable

---

# 16. Warm Buckets

Warm buckets are:

    Full Hot Buckets
    that have rolled over

They are:

- Still on fast storage
- Searchable
- No longer receiving new entries

### Flow

    HOT
      ↓
    Full
      ↓
    WARM

---

# 17. Cold Buckets

Cold buckets contain:

    Older Data

They are moved to:

- Cheap high-capacity mechanical storage
- Cloud object storage

They remain searchable.

However:

    Searching takes significantly longer.

### Memory

    COLD
     ↓
    Older Data
     ↓
    Cheaper Storage
     ↓
    Slower Search

---

# 18. Frozen Buckets

Frozen buckets contain:

    Expired Data

The data may be:

- Deleted entirely
- Compressed
- Archived off-site

Frozen data is:

    Unsearchable

without:

    Manual Re-indexing

---

# 19. Data Normalization — Splunk CIM

## CIM

**CIM = Common Information Model**

Different security products can use different field names for the same concept.

Example environment:

- Palo Alto Firewalls
- Zscaler Web Proxies
- AWS VPC Flow Logs

A connection block can look different in each system.

---

## Palo Alto

    action=deny
    src=192.168.1.50

## Zscaler

    block_type=policy_blocked
    client_ip=192.168.1.50

## AWS VPC

    log_status=REJECT
    srcaddr=192.168.1.50

All three represent:

    Connection Blocked

But they use different field names.

---

# 20. Problem Without Normalization

Suppose the SOC analyst wants to find:

    Blocked IPs

across the entire company.

Without normalization, the analyst would need a complex query that understands every vendor's:

- Vocabulary
- Field names
- Log structure

---

# 21. CIM Solution — Field Aliasing & Tagging

Splunk solves this using:

    Common Information Model (CIM)

During search-time execution:

    Data-Model Mappings
           ↓
    Run in Background
           ↓
    Vendor-Specific Fields
           ↓
    Standard Universal Fields

Example normalized fields:

    Action = "blocked"
    src_ip = "192.168.1.50"

---

# 22. Normalized Query

Because the data is normalized, one concise query can work across different security vendors.

Example:

    tag=network tag=communicate action=blocked src_ip=192.168.1.50

### Easy Understanding

Instead of writing separate queries for:

    Palo Alto
       +
    Zscaler
       +
    AWS

the analyst can use:

    One Standardized Query

---

# 23. Real-Time Correlation Engines

Once logs are:

- Indexed
- Normalized

the SIEM changes from:

    Passive Repository

into:

    Active Real-Time Threat Detection Engine

This is handled by:

    Correlation Searches

inside:

    Splunk Enterprise Security (ES)

---

# 24. Correlation Searches

Correlation Searches run automatically in the background.

Example schedule:

    Every 5 Minutes

checking:

    Previous 5 Minutes of Logs

They use:

    SPL
    Search Processing Language

---

# 25. Incident Review & Analysis

When a correlation search meets its defined conditions:

    Correlation Search
          ↓
    Conditions Match
          ↓
    Notable Event
          ↓
    Splunk Enterprise Security
          ↓
    Triage Pane
          ↓
    SOC Analyst

---

# 26. Notable Event

A matching correlation search creates a:

    Notable Event

inside the:

    Splunk Enterprise Security Triage Pane

This starts the human SOC investigation process.

---

# 27. Automatic Context Enrichment

The SIEM automatically extracts important fields such as:

- User
- `src_ip`
- Host

It then cross-references these against:

    Internal Corporate Lookups
    / Watchlists

in real time.

---

# 28. Example of Context Enrichment

Before the analyst even opens the ticket, the SIEM can identify:

### User

The account belongs to:

    VP of Global Finance

### Host

The targeted host contains:

    PCI-Compliant Financial Data

### Easy Understanding

Instead of showing only:

    Suspicious Activity

the SIEM adds context about:

- Who is involved
- Which source IP is involved
- Which host is involved
- What important data may be on the host

---

# 29. SIEM vs EDR

## Scope of Sight

### SIEM — Splunk Enterprise Security

    Global Enterprise

Covers:

- Cloud
- Network
- Identity
- Applications
- Endpoints

### EDR

    Localized Endpoint

Examples:

- Laptops
- Workstations
- Virtual Machine servers

---

## Primary Mechanism

### SIEM

Uses:

    Cross-Log Data Correlation
            +
    Complex Event Aggregation

### EDR

Uses:

    Deep OS Kernel Behavioral Inspection
            +
    Memory Tracking

---

## Data Types

### SIEM

Uses:

    Structured / Unstructured Logs

Through:

- Syslog
- JSON
- API
- Event Channels

### EDR

Uses:

    Native Raw Telemetry

Examples:

- Process creation
- File modification streams

---

# 30. SIEM vs EDR — Quick Comparison

| Capability | Splunk Enterprise Security (SIEM) | EDR |
|---|---|---|
| Scope of Sight | Global Enterprise: Cloud, Network, Identity, Applications, Endpoints | Localized Endpoint: Laptops, Workstations, Virtual Machine servers |
| Primary Mechanism | Cross-log data correlation and complex event aggregation | Deep OS kernel behavioral inspection and memory tracking |
| Data Types | Structured/Unstructured logs via Syslog, JSON, API, Event Channels | Native raw telemetry: process creation, file modification streams |

---

# 31. Complete SIEM Flow

    DATA SOURCES
         ↓
    Universal Forwarder
         ↓
    Collection
         ↓
    Heavy Forwarder
         ↓
    Filtering / Masking
         ↓
    Splunk Indexer
         ↓
    Parsing
         ↓
    Metadata
         ↓
    Bucket Storage
         ↓
    CIM Normalization
         ↓
    Correlation Search
         ↓
    Notable Event
         ↓
    Lookup / Watchlist Enrichment
         ↓
    SOC Analyst

---

# 32. Easy SIEM Memory

    SIEM

    COLLECT
       ↓
    PROCESS
       ↓
    STORE
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

---