# SOC Analyst L1 — Class 28

---

# ⚡ 30-SECOND RECALL

**Splunk** = Platform for searching, monitoring and analyzing machine-generated data.

Main architecture:

    FORWARDER
        ↓
    INDEXER
        ↓
    SEARCH HEAD
        ↓
    ANALYST

Easy memory:

    Forwarder → Collect
    Indexer → Parse + Store
    Search Head → Search + Display

Splunk uses:

    Schema-on-Read

---

# 🔥 MUST REMEMBER

## 1. Splunk

Splunk can:

- Capture data
- Index data
- Correlate data
- Store searchable data
- Generate graphs
- Generate reports
- Generate alerts
- Generate dashboards
- Generate visualizations

---

# 2. Forwarders

**Forwarder = Lightweight data collection agent**

Installed on:

- Endpoints
- Cloud containers
- Application servers

### Universal Forwarder

Example:

    Windows AD Controller
          ↓
    Windows Event Channel
          ↓
    Universal Forwarder
          ↓
    Security Event Logs
          ↓
    TCP 9997

---

# 3. Indexer

**Indexer = Splunk's processing and storage engine**

It:

1. Receives raw data
2. Splits it into events
3. Extracts timestamps
4. Adds metadata
5. Stores the data

Important metadata:

    host
    source
    sourcetype

### Memory

    host → Where?
    source → Source/file
    sourcetype → Data format

---

# 4. Bucket Lifecycle

    HOT
      ↓
    WARM
      ↓
    COLD
      ↓
    FROZEN

### Hot

- Active writing
- Fastest storage
- NVMe / SSD

### Warm

- Rotated from Hot
- No new entries
- Fast querying

### Cold

- Older data
- High-capacity/cheaper storage
- Mechanical disks / cloud object storage

### Frozen

- Expired data
- Based on retention policy
- Deleted OR moved to unindexed offline archive

---

# 5. Search Head

**Search Head = User interface**

It:

- Does not store logs
- Receives analyst queries
- Distributes workload to Indexers
- Aggregates results
- Displays results

Results can be:

- Tables
- Charts

### Flow

    Analyst Query
         ↓
    Search Head
         ↓
    Indexers
         ↓
    Results
         ↓
    Search Head
         ↓
    Tables / Charts

---

# 6. Schema-on-Write

Traditional databases such as:

- MySQL
- SQL Server

use:

    Schema-on-Write

Structure is defined before storing data:

- Tables
- Rows
- Columns
- Data types

If the log format changes unexpectedly, the database may reject it.

---

# 7. Schema-on-Read

Splunk uses:

    Schema-on-Read

Logs are kept in:

    Raw Native Text Format

Important fields extracted when data arrives:

    _time
    host
    source
    sourcetype

Other fields such as:

    user_id
    ip_address
    error_code

are extracted when the analyst searches.

Splunk uses:

    Regex

dynamically during the search.

---

# 8. Why Schema-on-Read Matters

Example:

    user_id
       ↓
    account_number

If the application changes the field:

### Traditional Database

May reject / lose the changed data.

### Splunk

Keeps the raw text.

The analyst can:

    Adjust Search Logic

---

# ⭐ INTERVIEW Q&A

## Q1. What is Splunk?

**Answer:**  
A platform for searching, monitoring and analyzing machine-generated data.

## Q2. What are the three main Splunk components?

**Answer:**

    Forwarder
    Indexer
    Search Head

## Q3. What does a Forwarder do?

**Answer:**  
Collects and securely forwards raw data.

## Q4. What does an Indexer do?

**Answer:**  
Parses data, extracts timestamps, adds metadata and stores it.

## Q5. What are the important metadata fields?

**Answer:**

    _time
    host
    source
    sourcetype

## Q6. What is the bucket lifecycle?

**Answer:**

    Hot → Warm → Cold → Frozen

## Q7. What does a Search Head do?

**Answer:**  
It provides the interface, distributes searches, aggregates results and displays them.

## Q8. What is Schema-on-Read?

**Answer:**  
Raw data is retained and additional fields are extracted when searching.

## Q9. What is Schema-on-Write?

**Answer:**  
The data structure is defined before data is stored.

## Q10. Why is Schema-on-Read useful?

**Answer:**  
It keeps raw data usable even when the log format changes.

---

# 🧠 SOC ANALYST MINDSET

Think:

    DATA
      ↓
    FORWARDER
      ↓
    INDEXER
      ↓
    SEARCH HEAD
      ↓
    ANALYST

When investigating Splunk data, remember:

    _time
    host
    source
    sourcetype

---

# 📝 QUESTION PAPER MODE

1. What is Splunk?
2. What are the three main Splunk components?
3. What does a Forwarder do?
4. What is a Universal Forwarder?
5. What is TCP 9997?
6. What does an Indexer do?
7. What are `host`, `source`, and `sourcetype`?
8. What is the bucket lifecycle?
9. What does a Search Head do?
10. What is Schema-on-Write?
11. What is Schema-on-Read?
12. Which fields are extracted when data arrives?
13. When are fields such as `user_id` and `ip_address` extracted?
14. Why is Schema-on-Read useful?

---

# ✅ ANSWER KEY

1. A platform for searching, monitoring and analyzing machine-generated data.
2. Forwarders, Indexers and Search Heads.
3. Collects and securely forwards raw data.
4. A lightweight agent that collects data from systems such as a Windows AD Controller.
5. TCP port used for the forwarding stream.
6. Parses, timestamps, adds metadata and stores data.
7. `host` = where from, `source` = source/file, `sourcetype` = data format.
8. Hot → Warm → Cold → Frozen.
9. Provides the interface, distributes searches, aggregates results and displays them.
10. Structure is defined before data is stored.
11. Raw data is retained and fields are extracted during search.
12. `_time`, `host`, `source`, `sourcetype`.
13. During the search using Regex.
14. Raw data remains usable even when the log format changes.

---

# 🧩 FINAL MEMORY MAP

    SPLUNK
       │
       ├── FORWARDER
       │      └── COLLECT
       │
       ├── INDEXER
       │      ├── PARSE
       │      ├── METADATA
       │      └── STORE
       │
       └── SEARCH HEAD
              ├── SEARCH
              ├── AGGREGATE
              └── DISPLAY

    STORAGE:
    HOT → WARM → COLD → FROZEN

    DATA MODEL:
    Schema-on-Read

---

# 🔥 30-SECOND FINAL REVISION

**Splunk** → Search + Monitor + Analyze

**Forwarder** → Collect + Send

**Indexer** → Parse + Store

**Search Head** → Search + Display

**TCP 9997** → Forwarding stream

**Metadata** → `_time`, host, source, sourcetype

**Buckets** → Hot → Warm → Cold → Frozen

**Schema-on-Read** → Fields extracted during search

---
