
# Windows Event Logs, Processes & Services

---

# 1. 30-Second Recall

## Windows Event Logs

- Windows Event Logs = Windows activity ka forensic timeline.
- Examples:
  - User login
  - Process start
  - Service start
  - Policy change

### Location

    C:\Windows\System32\winevt\Logs\

### Format

    .evtx

### Logs Answer

    WHO
    WHAT
    WHEN
    WHERE
    HOW

---

# 2. Windows Logging Architecture

    Action Happens
          ↓
    Event Provider
          ↓
    Windows Event Log Service
          ↓
    EVTX File
          ↓
    Event Viewer / SIEM

## Main Components

- Event Provider → Generates events
- Event Channel → Security / System / Application
- Event Log Service → Stores logs

## Main Log Types

- Security
- System
- Application
- Setup
- Forwarded Events

## Event Types

- Error
- Warning
- Information
- Success Audit
- Failure Audit

## View Logs Using

- Event Viewer
- Command Prompt
- PowerShell
- SIEM

---

# 3. Security Logs

Security Logs track:

- Authentication
- Authorization
- Privileges
- Account Changes

## Logon Types

| Type | Meaning | SOC Use |
|------|---------|---------|
| 2 | Interactive | Local Login |
| 3 | Network | SMB Access |
| 10 | Remote | RDP |
| 7 | Unlock | Session Reuse |

### SOC Formula

    Logon Type + IP + User
            ↓
       Attack Pattern

---

# 4. Must-Know Security Event IDs

## 🔥 MUST REMEMBER

| Event ID | Meaning |
|----------|---------|
| 4624 | Successful Logon |
| 4625 | Failed Logon |
| 4648 | Explicit Credentials |
| 4672 | Special Privileges |
| 4688 | Process Created ⭐ |
| 4720 | User Account Created |
| 4728 / 4732 | User Added to Group |
| 4768 | Kerberos TGT |
| 4769 | Kerberos Service Ticket |
| 4771 | Kerberos Pre-auth Failed |
| 4776 | NTLM Authentication |
| 1102 | Security Log Cleared ⭐ |
| 7045 | Service Installed ⭐ |

## Other Security IDs - Know for Reference

| Event ID | Meaning |
|----------|---------|
| 4634 | Logoff |
| 4647 | User Initiated Logoff |
| 4689 | Process Terminated |
| 4722 | Account Enabled |
| 4723 | Password Change Attempt |
| 4724 | Password Reset |
| 4725 | Account Disabled |
| 4726 | Account Deleted |
| 4729 | Removed from Global Group |
| 4733 | Removed from Local Group |
| 4756 | Added to Universal Group |
| 4757 | Removed from Universal Group |
| 4673 | Sensitive Privilege Used |
| 4674 | Privileged Object Operation |
| 4656 | Handle Requested |
| 4663 | Object Access Attempt |
| 4658 | Handle Closed |
| 4719 | Audit Policy Changed |
| 4739 | Domain Policy Changed |
| 4608 | Windows Started |
| 4609 | Windows Shutdown |
| 4616 | System Time Changed |

> Do NOT try to memorize every Event ID at once.
> First make the 🔥 IDs strong.

---

# 5. System Logs

System Logs track:

- OS behavior
- Drivers
- Hardware
- Boot events

## 🔥 Important System IDs

| Event ID | Meaning |
|----------|---------|
| 6005 | Event Log Service Started |
| 6006 | Event Log Service Stopped |
| 6008 | Unexpected Shutdown |
| 6013 | System Uptime |
| 41 | Kernel-Power |
| 1074 | Planned Shutdown/Restart |
| 109 | Kernel Power Critical Error |
| 219 | Driver Failed to Load |
| 225 | Device Not Migrated |
| 7 | Bad Block |
| 11 | Disk Controller Error |
| 15 | Device Not Ready |
| 51 | Disk Warning |
| 55 | NTFS Corruption |
| 98 | NTFS Volume Corruption |
| 7000 | Service Failed to Start |
| 7001 | Service Dependency Failed |
| 7009 | Service Timeout |
| 7011 | Service Timeout / No Response |
| 7034 | Service Crashed |
| 7036 | Service State Changed |
| 4201 | Network Adapter Connected |
| 4202 | Network Adapter Disconnected |
| 1014 | DNS Client Event |
| 1 | Time Synchronized |
| 36 | Time Service Error |
| 1000 | Application Error |
| 1001 | BugCheck / BSOD |
| 7045 | Service Installed |

### High-Priority Patterns

    41 + 6008 + 1001
        ↓
    Crash / Reboot Investigation

    7 / 11 / 51 / 55 / 98
        ↓
    Disk / File-System Problems

    7000 / 7034
        ↓
    Service Problems

    219 / 225
        ↓
    Driver Problems

    1014
        ↓
    DNS / Network Problem

---

# 6. Application Logs

Track:

- Application crashes
- Errors
- Software activity

### SOC Relevance

- Exploit attempts
- Malicious application behavior

Example:

    Word Crash
       ↓
    Possible Exploit
       ↓
    Investigate Context

## Application Event ID Groups

### Application

    1000 → Application Error
    1001 → Application Hang
    1002 → Application Unresponsive
    1003 → Application Restart
    1004 → Application Start
    1005 → Application Stop
    1006 → Application Crash
    1007 → Application Fault

### .NET

    1026 → .NET Runtime Error
    1027 → Warning
    1028 → Information
    1029 → Debug

### Installation / Configuration

    1030 → Application Install
    1031 → Application Uninstall
    1032 → Application Update
    1033 → Configuration Change
    1034 → Configuration Error

### Security / Permission

    1040 → Access Denied
    1041 → Invalid Credentials
    1042 → Login Failure
    1043 → Permission Change
    1044 → Security Error

### Performance / Resources

    1050 → Performance Warning
    1051 → Performance Error
    1052 → Resource Warning
    1053 → Resource Error
    1054 → Timeout

### Integration

    1060 → Service Communication Failure
    1061 → External System Error
    1062 → Message Queue Error
    1063 → Email Send Failure
    1064 → API Call Failure

### Audit / Logging

    1070 → Audit Success
    1071 → Audit Failure
    1072 → Log Write Success
    1073 → Log Write Failure

> Application Event IDs are mainly reference knowledge.
> Do not waste time memorizing all of them now.

---

# 7. Windows Process

## Definition

A process = Running instance of a program.

A process has:

- Memory space
- Threads
- Resources
- Security context

### Simple Flow

    Program on Disk
          ↓
       Execute
          ↓
    Process in Memory
          ↓
         PID

---

# 8. Components of a Process

## PID

- Process ID
- Unique identifier

Example:

    PID: 4321

## Virtual Memory

- Each process gets isolated memory.
- Can be abused in process injection.

## Threads

- Units of execution.
- One process can have multiple threads.

## Handles

References to system resources:

- Files
- Registry
- Network

## Security Context

Process runs as a user.

Examples:

- SYSTEM
- Administrator
- User

---

# 9. Windows Process Architecture

    System
      ↓
    smss.exe (Master)
      ↓
    Session 0 / Session 1
      ↓
    csrss.exe
    wininit.exe
      ├── services.exe
      │      ↓
      │   svchost.exe
      │
      ├── lsass.exe
      │
      └── lsaiso.exe

    winlogon.exe
      ↓
    userinit.exe
      ↓
    explorer.exe

---

# 10. Process Life Cycle

    New
     ↓
    Ready
     ↓
    Running
     ↓
    Terminated

### Waiting

A process may enter Waiting when waiting for:

- User input
- Network
- Signal
- OS scheduling

### States

- New → Process created
- Ready → Ready to run
- Running → Currently executing
- Waiting → Temporarily waiting
- Terminated → Process exits

---

# 11. Process Creation Flow

    User/System triggers execution
                ↓
          Win32 API called
                ↓
       Kernel creates process
                ↓
          Memory allocated
                ↓
          Threads created
                ↓
       Process starts execution

---

# 12. ⭐ Parent-Child Relationship

Every process is created by another process.

### Normal Example

    explorer.exe
         ↓
      chrome.exe

### Suspicious Example

    winword.exe
         ↓
    powershell.exe

### SOC Rule

Abnormal parent-child relationship

    ↓

Possible suspicious activity

---

# 13. Critical Windows Processes

| Process | Main Function |
|---------|---------------|
| System / ntoskrnl.exe | Windows kernel |
| smss.exe | Session Manager |
| csrss.exe | Client/Server Runtime |
| wininit.exe | Windows initialization |
| services.exe | Service Control Manager |
| lsass.exe | Authentication / Security |
| svchost.exe | Hosts Windows services |
| explorer.exe | Desktop / File Explorer |
| spoolsv.exe | Print Spooler |
| taskhostw.exe | Hosts scheduled tasks |
| dwm.exe | Desktop Window Manager |
| wuauclt.exe | Windows Update Client |
| MsMpEng.exe | Microsoft Defender |

### Critical Processes

- System
- smss.exe
- csrss.exe
- wininit.exe
- services.exe
- lsass.exe
- svchost.exe

### Safety

Do not terminate critical processes unnecessarily.

Possible results:

- Data loss
- System crash
- OS failure

### Check Before Ending Process

- File location
- Digital signature
- Description
- Associated services
- Resource usage
- Behavior

Expected locations:

    C:\Windows\System32
    C:\Windows

Expected signer:

    Microsoft Corporation

---

# 14. Windows Process Tree

### Normal

    smss.exe
     ├── csrss.exe
     ├── wininit.exe
     ├── services.exe
     ├── lsass.exe
     └── svchost.exe

### SOC

Any unexpected deviation

    ↓

Investigation

### Example

    winword.exe
         ↓
      cmd.exe
         ↓
    powershell.exe

---

# 15. Process Types

## User Processes

- Applications

## System Processes

- OS-level processes

## Background Processes

- Services

---

# 16. Process-Based Attacks

## Process Injection

Inject malicious code into another process.

    malware
       ↓
    inject
       ↓
    explorer.exe

### Indicators

- Suspicious child process
- Memory anomalies

## DLL Injection

- Malicious DLL injected into another process.

## Process Hollowing

    Start legitimate process
            ↓
    Replace process memory
            ↓
         Malware

Example:

    notepad.exe
         ↓
    Memory replaced
         ↓
       malware

## LOLBins

Living Off the Land Binaries = legitimate system tools abused for malicious activity.

Examples:

- powershell.exe
- cmd.exe
- rundll32.exe

### SOC Indicator

    powershell.exe
          ↓
    Encoded Command

---

# 17. Process Investigation Flow

## SOC Steps

    1. Identify process
       Event ID 4688
              ↓
    2. Check parent process
              ↓
    3. Check command line
              ↓
    4. Check user context
              ↓
    5. Check network activity
              ↓
    6. Correlate with logs

## Common Red Flags

- Word → PowerShell
- Browser → cmd.exe
- svchost.exe → unusual child
- Random executable → Temp folder

## SOC Mindset

Don't ask only:

    "What is this process?"

Ask:

    "Why is this process running?"
    "Who started it?"
    "What did it do next?"

---

# 18. Windows Services

## Definition

Windows Service:

- Runs in background
- Does not require user interaction
- Often starts automatically at boot

### Application vs Service

    Application
        ↓
    Needs User
        ↓
    Visible

    Service
        ↓
    Runs Silently
        ↓
    Background

## Legitimate Examples

- Windows Update
- Antivirus
- Print Spooler
- DHCP Client
- Remote Desktop Service

---

# 19. Service Control Manager

SCM = Service Control Manager

### Main Role

Central controller of Windows Services.

Responsibilities:

- Start services
- Stop services
- Manage service state
- Maintain service database

---

# 20. How Services Work Internally

    Windows Service Installer
              ↕
    Service Control Manager
              ↕
    Windows Service Database

    Windows Service Controller
              ↕
    Service Control Manager

    Windows Services in Execution
              ↕
    Service Control Manager

### Service Startup

    System Boot
        ↓
    SCM starts
        ↓
    SCM reads Registry
        ↓
    Loads Services
        ↓
    Services Start

---

# 21. Service Registry Location

    HKLM\SYSTEM\CurrentControlSet\Services

Each service contains:

- Service Name
- Image Path
- Start Type
- Permissions

---

# 22. Service Types

## Kernel Services

- Drivers

## File System Services

- Disk operations

## User-Mode Services

- Normal background services

---

# 23. Service Startup Types

| Type | Meaning |
|------|---------|
| Automatic | Starts at boot |
| Manual | Starts when needed |
| Disabled | Cannot start |

---

# 24. svchost.exe

## What is it?

A container process that hosts multiple services.

    svchost.exe
        ↓
    Multiple Services

### SOC Importance

- Malware may hide inside svchost.exe.
- Can be difficult to detect.

---

# 25. Services vs Processes

| Feature | Process | Service |
|---------|---------|---------|
| User Interaction | Yes | No |
| Runs | On Demand | Background |
| Persistence | No | Yes |

---

# 26. Service Attack Techniques

## Malicious Service Installation

Example:

    Service Name:
    UpdateService

    Path:
    C:\Users\Temp\malware.exe

Looks legitimate but may be malware.

## Service Hijacking

    legit.exe
        ↓
    replaced with
    malware.exe

## Privilege Escalation

If service runs as:

    SYSTEM

Attacker may obtain:

    Admin Access

## Persistence

    Malware installs Service
            ↓
        System Reboot
            ↓
       Service Runs Again

---

# 27. Real SOC Scenario

    4624 → Login
        ↓
    4688 → powershell.exe
        ↓
    7045 → New Service Installed
        ↓
    Initial Access
        ↓
    Execution
        ↓
    Persistence

### ⭐ Important Correlation

Do not investigate these events separately.

Correlate:

- User
- Time
- Process
- Service
- Timeline

---

# 28. Service Investigation Flow

    1. Identify Service
       Event ID 7045
              ↓
    2. Check Path
              ↓
    3. Check User Privileges
              ↓
    4. Check Parent Process
              ↓
    5. Check Related Logs
              ↓
    6. Correlate Timeline

## Red Flags

- New service created suddenly
- Service from Temp folder
- Random service name
- Service created after PowerShell

---

# 29. ⭐ Must Remember - Day 20

    Windows Event Logs
    → Forensic timeline

    Log Location
    → C:\Windows\System32\winevt\Logs\

    Log Format
    → .evtx

    Security Logs
    → Authentication
    → Authorization
    → Privileges
    → Account Changes

    4624
    → Successful Logon

    4625
    → Failed Logon

    4688
    → Process Created

    1102
    → Security Log Cleared

    7045
    → Service Installed

    Process
    → Running program

    Parent-Child
    → Very important for SOC

    Process Injection
    → Code injected into another process

    Process Hollowing
    → Legit process memory replaced

    LOLBins
    → Legitimate tools abused

    Service
    → Background program

    SCM
    → Controls Windows Services

    Service Registry
    → HKLM\SYSTEM\CurrentControlSet\Services

    Service Abuse
    → Persistence
    → Privilege Escalation

---

# 30. ⭐ Interview Q&A

## Q1. What are Windows Event Logs?

**Answer:**

Windows Event Logs are records of activities happening inside Windows and provide a forensic timeline for investigation.

---

## Q2. Where are Windows Event Logs stored?

**Answer:**

    C:\Windows\System32\winevt\Logs\

They use the `.evtx` format.

---

## Q3. What is Event ID 4624?

**Answer:**

Successful Logon.

---

## Q4. What is Event ID 4625?

**Answer:**

Failed Logon.

---

## Q5. What is Event ID 4688?

**Answer:**

Process Created.

It is important for investigating process execution.

---

## Q6. What is Event ID 1102?

**Answer:**

Security Log Cleared.

It may indicate evidence removal or log tampering.

---

## Q7. What is Event ID 7045?

**Answer:**

Service Installed.

It can be important for detecting service-based persistence.

---

## Q8. Why is parent-child process relationship important?

**Answer:**

It tells us which process started another process.

An abnormal relationship can indicate malicious execution.

Example:

    winword.exe
         ↓
    powershell.exe

---

## Q9. What is Process Injection?

**Answer:**

Injecting malicious code into another process.

---

## Q10. What is Process Hollowing?

**Answer:**

A legitimate process is started and its memory is replaced with malicious code.

---

## Q11. What are LOLBins?

**Answer:**

Legitimate Windows tools that attackers abuse for malicious activity.

Examples:

- PowerShell
- cmd
- rundll32

---

## Q12. What is a Windows Service?

**Answer:**

A background program that can run without user interaction and often starts automatically.

---

## Q13. What is SCM?

**Answer:**

Service Control Manager.

It controls Windows Services.

---

## Q14. Where are Windows Services stored?

**Answer:**

    HKLM\SYSTEM\CurrentControlSet\Services

---

## Q15. What is svchost.exe?

**Answer:**

A container process used to host multiple Windows services.

---

# 31. SOC Analyst Mindset

When you receive a Windows alert:

    1. What happened?
             ↓
    2. Which Event ID?
             ↓
    3. Which user?
             ↓
    4. Which IP?
             ↓
    5. Which process?
             ↓
    6. Who started it?
             ↓
    7. What command ran?
             ↓
    8. What happened next?
             ↓
    9. Any persistence?
             ↓
   10. Correlate timeline

### Golden Rule

Don't investigate one log alone.

    Event
      +
    User
      +
    IP
      +
    Process
      +
    Parent Process
      +
    Service
      +
    Timeline
      ↓
    Complete Attack Story

---

# 32. Question Paper Mode

## Questions Only

1. What are Windows Event Logs?
2. Where are Windows Event Logs stored?
3. What is the `.evtx` format?
4. What are the main Windows Event Log types?
5. What are Logon Types 2, 3, 7 and 10?
6. What does Event ID 4624 indicate?
7. What does Event ID 4625 indicate?
8. What does Event ID 4688 indicate?
9. What does Event ID 1102 indicate?
10. What does Event ID 7045 indicate?
11. What is a Windows process?
12. What are the main components of a process?
13. What is a PID?
14. What is the Windows process life cycle?
15. What is a parent-child process relationship?
16. Why is `winword.exe → powershell.exe` suspicious?
17. What is Process Injection?
18. What is DLL Injection?
19. What is Process Hollowing?
20. What are LOLBins?
21. What is the purpose of `svchost.exe`?
22. What is a Windows Service?
23. What is SCM?
24. Where are Windows Services stored?
25. What are the three Service Startup Types?
26. What is Service Hijacking?
27. How can a service provide persistence?
28. How can services be abused for privilege escalation?
29. What should a SOC Analyst check when Event ID 7045 appears?
30. Why should multiple Windows events be correlated?

---

# 33. Answer Key

1. A forensic timeline of activities occurring inside Windows.
2. `C:\Windows\System32\winevt\Logs\`
3. Windows Event Log file format.
4. Security, System, Application, Setup and Forwarded Events.
5. Type 2 = Interactive, Type 3 = Network, Type 7 = Unlock, Type 10 = Remote/RDP.
6. Successful Logon.
7. Failed Logon.
8. Process Created.
9. Security Log Cleared.
10. Service Installed.
11. A running instance of a program.
12. Memory, threads, resources and security context.
13. Process ID.
14. New → Ready → Running → Waiting → Terminated.
15. One process starts another process.
16. Word normally should not need to launch PowerShell; it can indicate malicious execution.
17. Injecting malicious code into another process.
18. Injecting a malicious DLL into another process.
19. Replacing the memory of a legitimate process with malicious code.
20. Legitimate system tools abused for malicious activity.
21. Hosts multiple Windows services.
22. A background program that can run without user interaction.
23. Service Control Manager.
24. `HKLM\SYSTEM\CurrentControlSet\Services`
25. Automatic, Manual, Disabled.
26. Replacing the executable path of an existing service with a malicious one.
27. A malicious service can start again after reboot.
28. Abusing a service running with high privileges such as SYSTEM.
29. Service path, user privileges, parent process, related logs and timeline.
30. Individual events may look normal; correlation can reveal the complete attack chain.

---

# Final 30-Second Revision

    4624 → Successful Login
    4625 → Failed Login
    4688 → Process Created
    1102 → Security Log Cleared
    7045 → Service Installed

    Process
    → Parent
    → Child
    → Command Line
    → User
    → Network

    Suspicious:
    Word → PowerShell
    Browser → cmd
    Random EXE → Temp
    svchost → Unusual Child

    Service
    → Background
    → SCM
    → Registry
    → Persistence
    → Privilege Escalation

    SOC Goal:
    Correlate Events
    → Build Timeline
    → Understand Attack Story
