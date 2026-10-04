# SOC Analyst L1 — Class 28
## Splunk — A Leading SIEM Solution

---

# 1. What is Splunk?

**Splunk** is a horizontal software platform designed for:

- Searching machine-generated big data
- Monitoring machine-generated big data
- Analyzing machine-generated big data
- Real-time analysis

Splunk:

- Captures data
- Indexes data
- Correlates data
- Stores data in a searchable repository

From this searchable repository, Splunk can generate:

- Graphs
- Reports
- Alerts
- Dashboards
- Visualizations

### Easy Understanding

Splunk takes large amounts of machine-generated data and makes it:

    Searchable
        ↓
    Analyzable
        ↓
    Useful for monitoring and security

In an enterprise network, Splunk acts as a central intelligence system that listens to digital activity such as:

- Server activity
- Login activity
- Rogue login attempts

---

# 2. Splunk Core Architecture

Splunk uses a:

    Distributed Architecture

The process of handling large datasets is divided into three main layers:

    1. Forwarders
    2. Indexers
    3. Search Heads

### Complete Flow

    Data
     ↓
    Forwarders
     ↓
    Indexers
     ↓
    Search Heads
     ↓
    Analyst

Each layer has a different responsibility.

---

# 3. Forwarders — Data Collection

## What are Forwarders?

Forwarders are:

    Lightweight Agents

They are installed directly on:

- Endpoints
- Cloud containers
- Application servers

Their main purpose is to:

    Consume raw file streams
           ↓
    Ship the data securely

---

## Universal Forwarder Example

A:

    Universal Forwarder

can sit on a:

    Windows Active Directory Controller

It:

1. Hooks into the Windows Event channel.
2. Collects security event logs.
3. Compresses the security event logs.
4. Sends them to the next tier.

The data is sent over:

    TCP Port 9997

### Easy Flow

    Windows AD Controller
            ↓
    Windows Event Channel
            ↓
    Universal Forwarder
            ↓
    Compress Security Logs
            ↓
       TCP 9997
            ↓
       Next Tier

---

# 4. Indexers — Data Parsing & Storage

## What is an Indexer?

The Indexer is the:

    Engine Room

of Splunk.

It receives:

    Raw Data Streams

Then it:

1. Splits the data into discrete events.
2. Extracts timestamps.
3. Adds metadata.
4. Saves the data into a time-series database.

---

## Metadata

The Indexer tags events with:

- `host`
- `source`
- `sourcetype`

### Easy Memory

    host
      → Where did the data come from?

    source
      → What is the source/file?

    sourcetype
      → What type/format is the data?

---

# 5. Splunk Storage Lifecycle

Splunk organizes data into physical directories on disk called:

    Buckets

There are four bucket stages:

    HOT
      ↓
    WARM
      ↓
    COLD
      ↓
    FROZEN

---

# 6. Hot Buckets

Hot buckets are:

- Open for active writes
- Currently receiving data
- Stored on the fastest storage

Storage mentioned:

- NVMe
- SSD

### Easy Memory

    HOT
     ↓
    Active Writing
     ↓
    Fast NVMe / SSD

---

# 7. Warm Buckets

Warm buckets are:

    Rotated out from Hot

They are:

- Optimized for fast querying
- No longer receiving new entries

### Flow

    HOT
      ↓
    Rotated Out
      ↓
    WARM

---

# 8. Cold Buckets

Cold buckets contain:

    Older Data

The data is moved to:

- High-capacity storage
- Cheaper mechanical disks
- Cloud object storage

### Easy Memory

    COLD
      ↓
    Older Data
      ↓
    Cheaper / High-Capacity Storage

---

# 9. Frozen Buckets

Frozen buckets contain:

    Expired Data

based on the configured:

    Retention Policy

Example:

    Data older than 1 year

Splunk can:

- Delete the data
- Move the data to an unindexed offline archive

### Easy Memory

    FROZEN
       ↓
    Expired Data
       ↓
    Delete
       OR
    Offline Archive

---

# 10. Search Heads — Data Analytics & Visualization

## What is a Search Head?

The Search Head is the:

    User Interface

It handles:

    Zero Log Storage

The Search Head does not store the logs itself.

---

## What happens when an analyst searches?

When an analyst logs into Splunk and enters a query:

    Analyst enters Query
           ↓
      Search Head
           ↓
    Distributes Workload
           ↓
       Indexers
           ↓
    Results Aggregated
           ↓
      Search Head
           ↓
    Results Displayed

The Search Head distributes the workload across available Indexers.

The Indexers process the search.

The Search Head then:

- Aggregates the results
- Displays the results to the analyst

Results can be displayed as:

- Tables
- Charts

---

# 11. Complete Three-Tier Splunk Architecture

    ┌──────────────────────┐
    │      FORWARDERS      │
    │    Data Collection   │
    └──────────┬───────────┘
               ↓
    ┌──────────────────────┐
    │       INDEXERS       │
    │ Parsing & Storage    │
    └──────────┬───────────┘
               ↓
    ┌──────────────────────┐
    │     SEARCH HEADS     │
    │ Analytics & Visuals  │
    └──────────┬───────────┘
               ↓
             Analyst

### Easy Memory

**Forwarder = Collect**

**Indexer = Parse + Store**

**Search Head = Search + Display**

---

# 12. Schema-on-Write vs Schema-on-Read

Splunk's data handling uses:

    Schema-on-Read

To understand it, first compare it with:

    Schema-on-Write

---

# 13. Traditional Databases — Schema-on-Write

Traditional relational databases such as:

- MySQL
- SQL Server

require:

    Schema-on-Write

This means the database requires the structure to be defined before data is saved.

You must define:

- Tables
- Rows
- Columns
- Data types

before storing the data.

### Problem

If the log format unexpectedly changes:

    Changed Log Format
          ↓
    Database may reject it

---

# 14. Splunk — Schema-on-Read

Splunk uses:

    Schema-on-Read

When logs arrive, Splunk keeps them in their:

    Raw Native Text Format

It only extracts a few mandatory fields when the data arrives.

These fields are:

- `_time`
- `host`
- `source`
- `sourcetype`

---

# 15. Fields Extracted During Search

Other fields inside the log are not calculated immediately.

Examples:

- `user_id`
- `ip_address`
- `error_code`

These fields are extracted when the analyst performs a:

    Search

Splunk uses:

    Regex Code

dynamically at the exact time the search is executed.

### Easy Flow

    Raw Log
       ↓
    Keep Native Text
       ↓
    Extract Basic Fields
       ↓
    Analyst Searches
       ↓
    Regex Runs Dynamically
       ↓
    Required Fields Isolated

---

# 16. Why Schema-on-Read Matters

Suppose an application changes a field:

    user_id
        ↓
    account_number

In a traditional database using Schema-on-Write, the changed format can cause problems such as:

    Database rejection / data loss

Splunk keeps the raw text safely.

The analyst can then:

    Adjust Search Logic

to work with the changed field.

### Easy Understanding

    Log Format Changes
           ↓
    Splunk Keeps Raw Data
           ↓
    Analyst Adjusts Search
           ↓
    Data Can Still Be Used

---

# 17. Important Splunk Concepts

## Forwarder

    Collects and securely sends raw data

## Indexer

    Parses and stores data

## Search Head

    Provides the search interface
    and displays results

## Bucket

    Physical directory used for Splunk data storage

## `_time`

    Extracted timestamp

## host

    Source host

## source

    Data source / file pathway

## sourcetype

    Data structure / type

## Schema-on-Read

    Fields are extracted when data is searched

---

# 18. Complete Splunk Flow

    ENDPOINT / SERVER /
    CLOUD CONTAINER /
    APPLICATION SERVER
             ↓
         FORWARDER
             ↓
      Raw Data Stream
             ↓
          INDEXER
             ↓
      Parse into Events
             ↓
    Extract Metadata
             ↓
     Store in Buckets
             ↓
        SEARCH HEAD
             ↓
       Analyst Query
             ↓
    Work Distributed to
          Indexers
             ↓
      Results Aggregated
             ↓
       Tables / Charts

---

# 19. Storage Flow

    New Data
       ↓
     HOT
       ↓
     WARM
       ↓
     COLD
       ↓
    FROZEN

### Remember

**Hot → Active writing**

**Warm → No new entries, fast querying**

**Cold → Older, cheaper storage**

**Frozen → Expired, deleted or offline archive**

---

# 20. Main Concept in One View

    SPLUNK
       │
       ├── FORWARDERS
       │      ↓
       │   Collect Data
       │
       ├── INDEXERS
       │      ↓
       │   Parse + Store
       │      ↓
       │   Buckets
       │      ├── Hot
       │      ├── Warm
       │      ├── Cold
       │      └── Frozen
       │
       └── SEARCH HEADS
              ↓
          Search
              ↓
          Aggregate
              ↓
          Display
              ↓
        Tables / Charts

---