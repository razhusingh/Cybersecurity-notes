# SOC Analyst L1 — Class 26
# Raju Recall Notes

## EDR — Endpoint Detection & Response

---

# ⚡ 30-SECOND RECALL

### EDR

**EDR = Endpoint Detection & Response**

EDR continuously monitors endpoints to:

    SEE → DETECT → INVESTIGATE → RESPOND

### EDR Architecture

    Endpoint
       ↓
    EDR Agent
       ↓
    Telemetry
       ↓
    Centralized Cloud Engine
       ↓
    Analysis

### EDR Telemetry

- Process executions
- Registry changes
- Network connections
- File modifications

### Detection

EDR uses:

- Behavioral analysis
- Machine Learning
- Threat Intelligence
- Behavioral heuristics

### Investigation

EDR provides:

- Historical timeline
- Process Tree
- Patient Zero / Root Cause

### Response

EDR can:

- Isolate host
- Terminate processes
- Use Remote Shell
- Remove malicious files
- Remove persistence

---

# 🔥 MUST REMEMBER

## 1. EDR Architecture

### Hub-and-Spoke Model

Lightweight agents are installed on:

- Laptops
- Servers
- Cloud VMs

They send telemetry to the:

    Centralized Cloud Engine

---

# 2. FOUR EDR STAGES

    1. Continuous Data Collection
              ↓
    2. Behavioral Analysis & Detection
              ↓
    3. Investigation & Threat Hunting
              ↓
    4. Automated & Manual Response

### Easy Memory

    COLLECT
       ↓
    DETECT
       ↓
    INVESTIGATE
       ↓
    RESPOND

---

# 3. EDR VISIBILITY

EDR collects telemetry about:

### Process Executions

    What application launched?
    Which process launched another process?

Example:

    word.exe
       ↓
    cmd.exe

### Registry Changes

Monitors registry modifications.

Example:

A program changes boot settings to remain on the system after reboot.

### Network Connections

Shows:

- Internal IPs
- External IPs

### File Modifications

Example:

    document.docx
         ↓
    document.locked

Large numbers of changed files can indicate ransomware behavior.

---

# 4. BEHAVIORAL DETECTION

EDR does not only ask:

    "What is this file called?"

It also asks:

    "What is this file/script doing?"

### Example

A script with an unknown name attempts to:

    Dump the OS password database
    from LSASS memory

EDR can flag the behavior.

### Remember

    Unknown Name
         ≠
    Automatically Safe

---

# 5. INVESTIGATION

When EDR detects an anomaly:

    Detection
       ↓
    Alert
       ↓
    Analyst Investigation

EDR keeps historical information.

This gives the analyst a:

    Historical Timeline

The analyst can trace the attack back to:

    Patient Zero

### Possible Entry Points

- Malicious email attachment
- Exploited unpatched application

---

# 6. EDR RESPONSE

For high-speed threats such as ransomware, EDR can perform:

    Automated Containment

Examples:

- Network isolation
- Process termination
- Cleanup/remediation

---

# 7. EDR vs TRADITIONAL ANTIVIRUS

| Traditional AV | EDR |
|---|---|
| Signature-based | Behavior-based |
| Focuses on known bad files | Focuses on what attackers do |
| Limited event logging | Continuous logging |
| Delete/quarantine file | Isolate host |
| Limited visibility | Process/script/memory visibility |
| No full historical timeline in the comparison | Historical timeline / Flight Recorder |

### Easy Memory

    AV
    ↓
    "Do I know this bad file?"

    EDR
    ↓
    "What is this activity doing?"

---

# 8. FILELESS ATTACKS

Traditional AV can be blind to attacks running in system memory.

Example:

    Malicious PowerShell Scripts

EDR provides visibility into:

- Volatile memory spaces
- Active script executions

---

# 9. PROCESS TREE

A Process Tree shows:

    "Who spawned whom?"

### Class Example

    outlook.exe
         ↓
    chrome.exe
         ↓
    invoice_9932.pdf.exe
         ↓
    cmd.exe
         ↓
    powershell.exe
      -ExecutionPolicy Bypass
      -Enc
      WwB...

### Investigation Meaning

- Outlook → email activity
- Chrome → browser activity
- `invoice_9932.pdf.exe` → suspicious executable
- `cmd.exe` → command-line wrapper
- PowerShell → malicious script execution

---

# 10. DOUBLE EXTENSION TRICK

File:

    invoice_9932.pdf.exe

The user may think:

    "It is a PDF."

But the actual file is:

    .exe

### Attack Flow

    invoice_9932.pdf.exe
           ↓
    User thinks PDF
           ↓
    User opens it
           ↓
    Executable runs

The class identifies this as a classic phishing technique.

---

# 11. POWERSHELL FLAGS

## -ExecutionPolicy Bypass

Tells Windows to:

    Ignore security restrictions on scripts

## -Enc

Means:

    Encoded

The script is represented by an encoded string.

Example:

    WwB...

The encoded content helps hide what the script does from basic text filters.

---

# 12. PAYLOAD ACTIONS

After decoding the script, the class shows two important actions:

### Registry Modification

The script writes to:

    HKCU\Software\Microsoft\Windows\CurrentVersion\Run

This provides:

    Persistence

So after reboot:

    System Reboots
         ↓
    Run Key Executes
         ↓
    Malware Launches Again

---

### LSASS Dumping

The script attempts to read:

    lsass.exe

LSASS:

    Local Security Authority Subsystem Service

The class describes LSASS memory as containing:

- User passwords
- Tokens

The attacker is attempting:

    Credential Theft

Those credentials could be used to:

    Hijack Other Identities

---

# 13. IMMEDIATE RESPONSE

## Step 1 — Network Isolation

    2 seconds

Select:

    Isolate Host

The laptop is disconnected from:

- Local office network
- Internet

Result:

    C2 Connection Drops

The attacker can no longer:

- Send commands
- Pull stolen data out

---

## Step 2 — Process Termination

    5 seconds

EDR terminates:

    powershell.exe
    cmd.exe

Result:

    Malicious Script Halted

---

## Step 3 — Remediation & Cleanup

    10 minutes

Using:

    Live Response Remote Shell

The analyst:

- Deletes `invoice_9932.pdf.exe`
- Removes the persistence registry key

---

# 14. POST-INCIDENT

After the endpoint is safe:

## Identity Check

The analyst checks the identity system.

Example:

    Microsoft Entra ID

Actions:

- Force password reset
- Revoke user sessions

### Why?

The attacker may have already obtained the user's credentials.

---

## Workbook Lookup

The analyst creates a Lookup containing:

- Malicious file hash
- IP address contacted by the script

Then performs a global query across the SOC Workbook.

### Purpose

Check whether another machine has:

    Downloaded the same file

### Flow

    File Hash + IP
          ↓
       Lookup
          ↓
    Global Workbook Query
          ↓
    Check Other Machines

---

# 15. SIEM INTEGRATION

Different security solutions protect different parts of the environment.

Examples:

- Firewalls
- DLPs
- Email Security Gateways
- IAMs
- EDRs

These are integrated with:

    SIEM
    Security Information and Event Management

The SIEM becomes the:

    Central Point of Investigation

### Flow

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
    SOC Investigation

---

# ⭐ INTERVIEW Q&A

## Q1. What is EDR?

**Answer:**  
EDR stands for Endpoint Detection and Response. It continuously monitors endpoints to detect, investigate and respond to threats.

## Q2. What is EDR telemetry?

**Answer:**  
Data collected from endpoint activity such as processes, registry changes, network connections and file modifications.

## Q3. What are the four main stages of EDR?

**Answer:**

1. Continuous Data Collection
2. Behavioral Analysis & Detection
3. Investigation & Threat Hunting
4. Automated & Manual Response

## Q4. What is the difference between traditional AV and EDR?

**Answer:**

    AV  → Known bad files / signatures
    EDR → Behavior + continuous visibility + response

## Q5. What is a Process Tree?

**Answer:**  
It shows the parent-child relationship between processes — essentially, who spawned whom.

## Q6. What is Patient Zero?

**Answer:**  
The root cause/original point from which the attack can be traced.

## Q7. What does `-ExecutionPolicy Bypass` indicate?

**Answer:**  
It tells Windows to ignore script execution restrictions.

## Q8. What does `-Enc` mean?

**Answer:**  
Encoded. It indicates an encoded PowerShell command/script.

## Q9. Why is `invoice_9932.pdf.exe` suspicious?

**Answer:**  
It uses a double extension to make an executable appear like a PDF.

## Q10. What is the purpose of the Run registry key?

**Answer:**  
It provides persistence so the malware can launch again after reboot.

## Q11. Why is LSASS targeted?

**Answer:**  
The class describes LSASS memory as containing user passwords and tokens, making it a target for credential theft.

## Q12. What can EDR do during containment?

**Answer:**

- Isolate the host
- Terminate malicious processes
- Use Live Response for cleanup

## Q13. What is the purpose of the Workbook Lookup after the incident?

**Answer:**  
To check whether other machines in the enterprise downloaded the same malicious file or communicated with the relevant IP.

## Q14. What is the role of SIEM in this class?

**Answer:**  
It acts as the central point of investigation by bringing information from security solutions together.

## Q15. What is the basic EDR flow?

**Answer:**

    Collect
       ↓
    Detect
       ↓
    Investigate
       ↓
    Respond
       ↓
    Remediate

---

# 🧠 SOC ANALYST MINDSET

When an EDR alert appears, think:

    ALERT
      ↓
    What process started?
      ↓
    Who spawned it?
      ↓
    Process Tree
      ↓
    What command was executed?
      ↓
    Is it encoded?
      ↓
    What did the script change?
      ↓
    Network connections?
      ↓
    Credentials targeted?
      ↓
    Isolate
      ↓
    Terminate
      ↓
    Remediate
      ↓
    Check identity
      ↓
    Search other machines

### Remember

**Don't look at only the suspicious process.**

Look at its:

- Parent
- Child
- Command
- Behavior
- Network activity
- Persistence
- Credential activity

---

# 📝 QUESTION PAPER MODE

1. What is EDR and what is its purpose?

2. What are the four main stages of EDR?

3. What types of telemetry does an EDR agent collect?

4. What is the difference between traditional AV and EDR?

5. What is behavioral detection?

6. What is a Process Tree?

7. Why is `invoice_9932.pdf.exe` suspicious?

8. What do `-ExecutionPolicy Bypass` and `-Enc` indicate?

9. What is the purpose of the Run registry key?

10. Why is LSASS targeted in the class example?

11. What are the three immediate response steps?

12. What is the purpose of the Identity Check after containment?

13. Why is a Workbook Lookup performed after the incident?

14. What is Patient Zero?

15. What role does SIEM play in the described security architecture?

---

# ✅ ANSWER KEY

1. EDR is Endpoint Detection and Response; it continuously monitors endpoints to detect, investigate and respond to threats.

2. Continuous Data Collection, Behavioral Analysis & Detection, Investigation & Threat Hunting, Automated & Manual Response.

3. Process executions, registry changes, network connections and file modifications.

4. AV mainly uses known signatures and traditional file-based protection; EDR focuses on behavior, continuous visibility, investigation and response.

5. Detecting suspicious activity based on what the activity does rather than only its file name/signature.

6. A view showing the parent-child relationship of processes — who spawned whom.

7. It uses a double extension to make an executable appear like a PDF.

8. `-ExecutionPolicy Bypass` bypasses script execution restrictions; `-Enc` indicates an encoded command.

9. To provide persistence so the malware can execute again after reboot.

10. The class describes LSASS memory as containing user passwords and tokens, making it a target for credential theft.

11. Network isolation, process termination and remediation/cleanup.

12. To protect the user's identity by forcing a password reset and revoking sessions.

13. To check whether other machines downloaded the same malicious file or communicated with the relevant IP.

14. The root cause/original point from which the attack can be traced.

15. SIEM acts as the central point of investigation by bringing information from different security solutions together.

---

# 🧩 FINAL MEMORY MAP

    EDR
     │
     ├── COLLECT
     │     ├── Processes
     │     ├── Registry
     │     ├── Network
     │     └── Files
     │
     ├── DETECT
     │     ├── Behavior
     │     ├── ML
     │     └── Threat Intel
     │
     ├── INVESTIGATE
     │     ├── Alert
     │     ├── Process Tree
     │     ├── Timeline
     │     └── Patient Zero
     │
     └── RESPOND
           ├── Isolate
           ├── Kill Process
           ├── Cleanup
           ├── Identity Check
           └── Enterprise Search

---

# 🔥 FINAL 1-MINUTE REVISION

**EDR = Endpoint Detection & Response**

**Telemetry = Endpoint activity data**

**Process Tree = Who spawned whom**

**Behavioral Detection = What is it doing?**

**Patient Zero = Root cause/original attack point**

**Flight Recorder = Historical timeline**

**Double Extension = `invoice_9932.pdf.exe`**

**`-ExecutionPolicy Bypass` = Bypass script restrictions**

**`-Enc` = Encoded**

**Run Key = Persistence**

**LSASS = Credential target in the class example**

**Isolation = Cut network communication**

**Process Termination = Stop malicious execution**

**Live Response = Remote cleanup**

**Workbook Lookup = Search for the same threat across machines**

**SIEM = Central Investigation Point**

---