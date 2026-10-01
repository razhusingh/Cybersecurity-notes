# SOC Analyst L1 — Class 26

## Topic: EDR — Endpoint Detection & Response

---

# 1. EDR — Endpoint Detection & Response

## What is EDR?

**EDR = Endpoint Detection and Response**

EDR is an endpoint security solution that continuously monitors end-user devices to:

- Detect cyber threats
- Respond to cyber threats

Examples of threats mentioned:

- Ransomware
- Malware

EDR is also referred to as:

    Endpoint Detection and Threat Response (EDTR)

### Easy Understanding

EDR continuously watches what is happening on an endpoint and helps the security team:

    Monitor
       ↓
    Detect
       ↓
    Investigate
       ↓
    Respond

---

# 2. EDR Architecture

EDR operates on a simple:

    Hub-and-Spoke Model

## Endpoint Agent

Light agents are installed directly on endpoints such as:

- Laptops
- Servers
- Cloud VMs

These agents collect and stream telemetry back to a:

    Centralized Cloud Engine

The centralized cloud engine performs heavy-duty analysis.

### Easy Flow

    Laptop / Server / Cloud VM
             ↓
        EDR Agent
             ↓
         Telemetry
             ↓
    Centralized Cloud Engine
             ↓
          Analysis

---

# 3. Examples of EDR Solutions

The PDF mentions these EDR solutions:

- CrowdStrike Falcon
- SentinelOne ActiveEDR
- Microsoft Defender for Endpoint
- OpenEDR
- Symantec EDR

There are several other EDR solutions available.

Their underlying architecture is mostly similar, but their features may vary.

---

# 4. EDR Example — Visibility, Detection & Response

The PDF gives a simple example showing three important EDR capabilities.

## Visibility

EDR records:

- A PDF being opened
- A hidden background script being launched

### Easy Meaning

EDR can see what happens on the endpoint.

---

## Detection

EDR analyzes the script's behavior.

It recognizes the behavior as:

    Credential Theft

Then it fires an alert.

---

## Response

EDR can automatically:

- Isolate the laptop from the network
- Kill the malicious script

### Complete Flow

    PDF Opened
        ↓
    Hidden Script Launched
        ↓
    EDR Sees Activity
        ↓
    Behavioral Analysis
        ↓
    Credential Theft Detected
        ↓
    Alert
        ↓
    Laptop Isolated
        ↓
    Script Killed

---

# 5. How EDR Works — The Operational Flow

EDR continuously loops through a four-stage lifecycle to help keep the environment secure.

The four stages are:

1. Continuous Data Collection
2. Behavioral Analysis & Detection
3. Investigation & Threat Hunting
4. Automated & Manual Response

---

# 6. Stage 1 — Continuous Data Collection (Telemetry)

The endpoint agent records fundamental actions taking place on the operating system.

This collected information is called:

    Telemetry

## Types of Telemetry

### 6.1 Process Executions

EDR records:

- What applications are launching?
- Which process launched another process?

### Example

    word.exe
        ↓
    cmd.exe

The analyst can investigate whether `cmd.exe` was opened by `word.exe`.

---

## 6.2 Registry Changes

EDR monitors registry modifications.

### Example

A program may try to modify boot settings so that it can:

    Stay on the system after reboot

---

## 6.3 Network Connections

EDR records what network connections the machine is making.

It can show:

- Internal IP addresses
- External IP addresses

### Easy Meaning

The analyst can see:

    Which IP addresses
    is this machine talking to?

---

## 6.4 File Modifications

EDR monitors file changes.

### Example

Thousands of documents suddenly change their extensions to:

    .locked

This can indicate:

    Ransomware behavior

---

# 7. Stage 2 — Behavioral Analysis & Detection

The EDR cloud console receives the large amount of telemetry collected from endpoints.

Instead of only checking static file signatures, EDR analyzes the data using:

- Advanced behavioral models
- Machine Learning
- Threat Intelligence feeds

---

# 8. Behavioral Heuristics

Behavioral heuristics are an important part of EDR detection.

## Easy Understanding

EDR does not only ask:

    "What is the file/script called?"

It also asks:

    "What is the file/script doing?"

### Example

A script may have a completely new or unknown name.

EDR can still detect suspicious behavior.

If the script attempts to:

    Dump the OS password database
    from LSASS memory

EDR can flag it based on its behavior.

### Important Idea

    Unknown Name
         ≠
    Automatically Safe

EDR focuses on:

    What it is doing

rather than only:

    What it is named

---

# 9. Stage 3 — Investigation & Threat Hunting

When the detection engine identifies an anomaly:

    Detection
       ↓
    Alert
       ↓
    Analyst Investigation

The EDR records historical information.

This gives analysts a:

    Historical Timeline

---

## Patient Zero

The analyst can trace the attack back to its:

    Root Cause

The PDF refers to this as:

    Patient Zero

This helps determine how the attacker initially got in.

### Possible Entry Examples Mentioned

- Downloaded malicious email attachment
- Exploited an unpatched application

---

# 10. Stage 4 — Automated & Manual Response

This is where the:

    "R" in EDR

becomes important.

If EDR detects an active, high-speed threat such as:

    Ransomware

it does not necessarily wait for a human analyst.

It can execute:

    Automated Containment Actions

instantly.

---

# 11. Real-World EDR Workflow

The Class 26 visual workflow shows four major stages.

## 1. Continuous Visibility & Collection

Telemetry is collected from:

- Process executions
- Network connections
- Registry changes
- File modifications

The EDR agent collects telemetry from:

- Endpoint
- Server
- Cloud VM

---

## 2. Intelligent Detection & Analysis

The EDR cloud/central management analyzes the collected telemetry.

The visual shows examples such as:

- Credential dumping
- Malicious execution
- Fileless script activity
- Suspicious processes

The cloud engine uses:

- Behavioral detection
- ML / AI

to identify anomalies and behaviors.

---

## 3. Immediate Response & Containment

When a high-severity alert is generated, response actions can include:

- Network isolation
- SOC analyst actions
- Terminating malicious processes

The endpoint can be isolated from:

- Local network
- Internet

---

## 4. Eradication & Recovery

After containment, the analyst can:

- Remove malicious files
- Remove malicious registry keys
- Clean and remediate the endpoint

### Complete Workflow

    1. Data Collection
           ↓
    2. Behavioral Detection
           ↓
    3. Containment
           ↓
    4. Remediation
           ↓
    Clean & Remediated System

---

# 12. EDR vs Traditional Antivirus

| Feature | Traditional Antivirus (AV) | Endpoint Detection & Response (EDR) |
|---|---|---|
| Detection Method | Signatures — knows what bad files look like | Behaviors — knows what bad actors do |
| Data Retention | Only logs when something is blocked | Logs everything continuously, even benign data |
| Visibility | Blind to sophisticated fileless or living-off-the-land attacks | Full visibility into memory injections and scripts |
| Response Options | Delete or quarantine a single file | Isolate hosts, terminate processes, remote shell |

---

# 13. Detection Method — AV vs EDR

## Traditional Antivirus

Uses:

    Signatures

It knows what known bad files look like.

---

## EDR

Uses:

    Behaviors

It focuses on what bad actors are doing.

### Easy Memory

    AV
    ↓
    "Do I know this bad file?"

    EDR
    ↓
    "What is this activity doing?"

---

# 14. Data Retention — AV vs EDR

## Traditional Antivirus

Only logs an event when:

    A known virus is blocked

---

## EDR

Logs system activity continuously:

    24/7

This includes:

- Processes
- Network activity
- Registry activity

Even benign data can be logged.

---

# 15. Visibility — AV vs EDR

## Traditional Antivirus

Can be blind to sophisticated:

- Fileless attacks
- Living-off-the-land attacks

---

## EDR

Provides visibility into:

- Memory injections
- Scripts

---

# 16. Response Options — AV vs EDR

## Traditional Antivirus

Can:

- Delete a file
- Quarantine a file

---

## EDR

Can:

- Isolate hosts
- Terminate processes
- Provide remote shell

---

# 17. Feature-by-Feature Comparison

## Primary Goal

### Traditional Antivirus

    Prevention

Goal:

    Stop known malware from executing.

### EDR

    Detection & Response

Goal:

    Spot active threats
    +
    Provide tools to fight them

---

# 18. Data Logging

## Traditional Antivirus

Logging is:

    Passive

It only logs an event when a known virus is blocked.

---

## EDR

Logging is:

    Continuous

It logs all system activity:

- Processes
- Network
- Registry

continuously.

---

# 19. Response Actions

## Traditional Antivirus

Can:

- Quarantine a single file
- Delete a single file

---

## EDR

Can:

- Isolate hosts from the network
- Kill live processes
- Provide remote shell

---

# 20. Fileless Attacks

## Traditional Antivirus

The PDF describes traditional AV as:

    Blind

to attacks running purely in system memory.

### Example

    Malicious PowerShell Scripts

---

## EDR

Provides:

    Full Visibility

into:

- Volatile memory spaces
- Active script executions

---

# 21. Historical Data

## Traditional Antivirus

No historical timeline is available in the described comparison.

If an incident happens, the analyst cannot trace how the malware got there.

---

## EDR

Provides a:

    Flight Recorder

This provides a full timeline of events leading up to the attack.

### Easy Meaning

The analyst can look backward and understand:

    What happened?
        ↓
    What happened before it?
        ↓
    How did the attack begin?

---

# 22. Analyzing the EDR Process Tree

The SIEM triggers a high-severity alert:

    "Suspicious PowerShell Execution Detected."

The analyst needs to understand:

- How did this happen?
- What did the attacker do?
- How can the attacker be stopped?
- Could the attacker move laterally to other machines?

To investigate this, the analyst opens the:

    EDR Console

and views the:

    Process Tree

---

# 23. What is a Process Tree?

The Process Tree shows the:

    "Family Tree"

of process execution.

It shows:

    Who spawned whom

### Process Tree from the Class

    [1] outlook.exe
            ↓
    [2] chrome.exe
            ↓
    [3] invoice_9932.pdf.exe
            ↓
    [4] cmd.exe
            ↓
    [5] powershell.exe
        -ExecutionPolicy Bypass
        -Enc
        WwB...

---

# 24. Process Tree Breakdown

## Step 1 — outlook.exe

This is the:

    Email Client

The user received an email.

---

## Step 2 — chrome.exe

The user:

- Clicked a link
- Opened the browser

---

## Step 3 — invoice_9932.pdf.exe

A downloaded file was pretending to be a PDF.

The filename is:

    invoice_9932.pdf.exe

---

## Step 4 — cmd.exe

The downloaded file spawned:

    cmd.exe

This acts as a command-line wrapper.

---

## Step 5 — powershell.exe

PowerShell was launched with:

    -ExecutionPolicy Bypass

and:

    -Enc

followed by an encoded string:

    WwB...

This represents the malicious script.

---

# 25. Double Extension Trick

The file is named:

    invoice_9932.pdf.exe

Windows often hides the:

    .exe

extension by default.

Therefore, the user may think:

    "I am opening a PDF."

But the actual file is an executable.

### Attack Flow

    invoice_9932.pdf.exe
            ↓
    User thinks it is a PDF
            ↓
    User opens it
            ↓
    Executable runs

The PDF identifies this as a classic:

    Phishing

technique.

---

# 26. PowerShell Command Flags

The PowerShell command contains two important flags.

## -ExecutionPolicy Bypass

This tells Windows to:

    Ignore security restrictions on scripts

---

## -Enc

`-Enc` stands for:

    Encoded

It means the attacker has obfuscated the script into a large string of random-looking characters.

Example shown:

    WwB...

### Purpose

The encoded content helps hide what the script does from basic text filters.

---

# 27. Decoding the Payload

Using EDR tools, the analyst decodes the obfuscated script.

The script attempts two important actions on the host operating system:

1. Registry Modification
2. LSASS Dumping

---

# 28. Registry Modification

The script writes a key to:

    HKCU\Software\Microsoft\Windows\CurrentVersion\Run

This is a:

    Persistence Mechanism

## Why?

It ensures that even if the user restarts the laptop:

    System Reboots
          ↓
    Run Key Executes
          ↓
    Malware Launches Again

---

# 29. LSASS Dumping

The script attempts to read the memory space of:

    lsass.exe

LSASS stands for:

    Local Security Authority Subsystem Service

The PDF describes LSASS memory as containing:

- User passwords
- Tokens

The attacker is trying to:

    Steal Credentials

The stolen credentials could then be used to:

    Hijack Other Identities

---

# 30. Immediate Response Action

At this stage:

- The attacker has active code execution.
- The attacker is trying to harvest passwords.

The EDR containment playbook is executed directly from the console.

Three response steps are shown.

---

# 31. Step 1 — Network Isolation

### Time

    2 seconds

The analyst selects:

    Isolate Host

The laptop is immediately disconnected from:

- Local office network
- Internet

### Result

The attacker's:

    Command-and-Control (C2)

connection drops.

The attacker can no longer:

- Send commands
- Pull stolen data out

### Flow

    Isolate Host
         ↓
    Network Connection Cut
         ↓
    C2 Connection Drops
         ↓
    Attacker Loses Communication

---

# 32. Step 2 — Process Termination

### Time

    5 seconds

The analyst uses EDR to kill:

    powershell.exe
    cmd.exe

### Result

The active malicious script is completely halted.

---

# 33. Step 3 — Remediation & Cleanup

### Time

    10 minutes

Using:

    Live Response Remote Shell

the analyst securely connects to the isolated machine.

The analyst:

- Deletes `invoice_9932.pdf.exe`
- Removes the persistence registry key created by the script

---

# 34. Closing the Loop — Post-Incident

After the asset is safe, the response does not simply stop.

The class connects the incident back to other concepts learned earlier.

Two important actions are performed:

1. Identity Check
2. Workbook Lookup

---

# 35. Identity Check

The analyst pivots to an:

    Identity Tool

Example:

    Microsoft Entra ID

The analyst:

- Forces a password reset
- Revokes the user's sessions

## Why?

The attacker may have:

    Scraped the user's credentials

before the malicious process was stopped.

---

# 36. Workbook Lookup

The analyst creates a Lookup containing:

- Malicious file hash
- IP address the script tried to communicate with

Then the analyst runs a global query across the:

    SOC Workbook

### Purpose

To check whether any other machine in the entire enterprise has:

    Downloaded the same file

### Easy Flow

    Malicious File Hash
            +
    Malicious IP
            ↓
        Lookup
            ↓
    Global Workbook Query
            ↓
    Check Other Machines

---

# 37. Result of the EDR Response

The class describes how EDR can transform:

    Potential Company-Wide Disaster
            ↓
    15-Minute Contained Incident

The response includes:

- Network isolation
- Process termination
- Remediation and cleanup
- Identity protection
- Enterprise-wide lookup

---

# 38. Security Solutions + SIEM

Within a network, different security solutions protect different components.

The class mentions:

- Firewalls
- DLPs
- Email Security Gateways
- IAMs
- EDRs
- Other security solutions

To:

    Minimize Effort
    +
    Maximize Efficiency

these security solutions are integrated with a:

    SIEM
    Security Information and Event Management

---

# 39. SIEM as the Central Investigation Point

The integrated security solutions send information into the SIEM.

The SIEM becomes:

    Central Point of Investigation

for analysts.

### Easy Flow

    Firewalls
        +
    DLP
        +
    Email Security Gateway
        +
    IAM
        +
    EDR
        ↓
       SIEM
        ↓
    Central Investigation Point
        ↓
    SOC Analyst

---

# 40. Complete Class 26 EDR Flow

    ENDPOINT
       ↓
    EDR Agent
       ↓
    Continuous Telemetry
       ↓
    Cloud / Central Analysis
       ↓
    Behavioral Detection
       ↓
    Alert
       ↓
    Investigation
       ↓
    Process Tree
       ↓
    Containment
       ↓
    Network Isolation
       ↓
    Process Termination
       ↓
    Remediation & Cleanup
       ↓
    Identity Check
       ↓
    Workbook Lookup
       ↓
    Enterprise-Wide Check
       ↓
    SIEM / Central Investigation

---

# 41. Easy Understanding of EDR

## EDR Basically Does Four Things

### 1. SEE

Collects endpoint telemetry.

    Processes
    Network
    Registry
    Files

### 2. DETECT

Analyzes behavior using:

    Behavioral Models
    ML
    Threat Intelligence

### 3. RESPOND

Can:

    Isolate Host
    Kill Process
    Remote Shell

### 4. INVESTIGATE

Provides:

    Historical Timeline
    Process Tree
    Root Cause
    Patient Zero

---

# 42. Important Terms from the Class

| Term | Easy Meaning |
|---|---|
| EDR | Endpoint Detection & Response |
| Telemetry | Data collected from endpoint activity |
| Behavioral Analysis | Detecting based on what activity does |
| Behavioral Heuristics | Identifying suspicious behavior even if the name is unknown |
| Patient Zero | Root cause/original point of the attack |
| Process Tree | Shows who spawned whom |
| Fileless Attack | Attack running in system memory rather than a normal file |
| Flight Recorder | Historical timeline of events |
| Network Isolation | Disconnecting the endpoint from network/internet |
| Process Termination | Stopping malicious processes |
| Live Response Remote Shell | Remote connection to the isolated machine for cleanup |
| C2 | Command-and-Control server/connection |
| Persistence | Mechanism allowing malware to remain/relaunch |
| LSASS | Local Security Authority Subsystem Service |
| SIEM | Security Information and Event Management |

---

# 43. Final Concept Map

    EDR
     │
     ├── VISIBILITY
     │      ↓
     │   Telemetry
     │      ├── Processes
     │      ├── Network
     │      ├── Registry
     │      └── Files
     │
     ├── DETECTION
     │      ↓
     │   Behavioral Analysis
     │      ├── ML
     │      ├── Threat Intel
     │      └── Behavioral Heuristics
     │
     ├── INVESTIGATION
     │      ↓
     │   Alert
     │      ↓
     │   Process Tree
     │      ↓
     │   Historical Timeline
     │      ↓
     │   Patient Zero
     │
     └── RESPONSE
            ↓
        Network Isolation
            ↓
        Process Termination
            ↓
        Cleanup
            ↓
        Recovery

---

# 44. EDR vs Antivirus — Quick Memory

    Traditional AV
          ↓
    Known Bad Files
          ↓
    Signature-Based
          ↓
    Block / Quarantine

            VS

    EDR
          ↓
    What Bad Actors Do
          ↓
    Behavioral Detection
          ↓
    Continuous Visibility
          ↓
    Investigate
          ↓
    Isolate
          ↓
    Kill Process
          ↓
    Remote Shell
          ↓
    Remediate

---