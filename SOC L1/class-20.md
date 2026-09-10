# Day 20 - Windows Event Logs, Processes & Services

---

# 1. Windows Event Logs

## What are Windows Event Logs?

Windows Event Logs are a forensic timeline of everything happening inside Windows.

Every action generates telemetry.

Examples:

- User login → Event generated
- Process starts → Event generated
- Service starts → Event generated
- Policy change → Event generated

## Where Logs Are Stored

    C:\Windows\System32\winevt\Logs\

### File Format

    .evtx

## Why Event Logs Are Critical for SOC

Logs answer:

- WHO
- WHAT
- WHEN
- FROM WHERE
- HOW

Without logs:

    No investigation

---

# 2. Windows Logging Architecture

## Event Logging Flow

    Action Happens
    (Login / Process / Service)
            ↓
    Event Provider
            ↓
    Windows Event Log Service
            ↓
    EVTX File
            ↓
    Event Viewer / SIEM

## Event Provider

Generates logs/events.

Examples:

- Security Provider
- PowerShell

## Event Channels / Log Types

Main channels:

- Security
- System
- Application
- Setup
- Forwarded Events

## Event Log Service

- Collects and stores Windows event logs.

---

# 3. Windows Event Log Types

Windows Event Logs contain different event types:

- Error
- Warning
- Information
- Success Audit
- Failure Audit

---

# 4. Ways to View Windows Logs

Logs can be viewed using:

- Event Viewer GUI
- Command Prompt
- PowerShell
- SIEM

---

# 5. Security Logs

## What are Security Logs?

Security logs track:

- Authentication
- Authorization
- Privileges
- Account changes

These are the primary investigation logs for a SOC Analyst.

---

# 6. Logon Types

Logon Type tells how the user/session logged in.

| Logon Type | Meaning | SOC Use |
|------------|---------|---------|
| 2 | Interactive | Local login |
| 3 | Network | SMB access |
| 10 | Remote | RDP |
| 7 | Unlock | Session reuse |

## SOC Mapping

    Logon Type + IP + User
              ↓
        Attack Pattern

---

# 7. Security Event Logs - Key Event IDs

## 7.1 Logon & Authentication Events

| Event ID | Description |
|----------|-------------|
| 4624 | Successful Logon |
| 4625 | Failed Logon |
| 4634 | Logoff |
| 4647 | User Initiated Logoff |
| 4648 | Logon Using Explicit Credentials |
| 4672 | Special Privileges Assigned |

### SOC Use

- 4624 → Successful login
- 4625 → Detect brute force / credential stuffing
- 4648 → Possible credential abuse
- 4672 → Special privileges assigned

### Important

Always check Logon Type for accurate detection.

---

# 8. Account Management Events

| Event ID | Description |
|----------|-------------|
| 4720 | User Account Created |
| 4722 | Account Enabled |
| 4723 | Password Change Attempt |
| 4724 | Password Reset by Admin |
| 4725 | Account Disabled |
| 4726 | Account Deleted |

### SOC Use

Monitor unexpected:

- Account creation
- Account enable/disable
- Password changes
- Password resets
- Account deletion

---

# 9. Group & Privilege Management Events

These help detect:

- Privilege escalation
- Group membership changes

| Event ID | Description |
|----------|-------------|
| 4728 | Member Added to Global Group |
| 4729 | Member Removed from Global Group |
| 4732 | Member Added to Local Group |
| 4733 | Member Removed from Local Group |
| 4756 | Member Added to Universal Group |
| 4757 | Member Removed from Universal Group |

## Critical Focus

Adding a user to:

- Administrators
- Domain Admins

is a high-risk event.

---

# 10. Process Creation & Execution Events

| Event ID | Description |
|----------|-------------|
| 4688 | Process Created |
| 4689 | Process Terminated |

## Event ID 4688

Most important event for process creation.

Can help track:

- New process
- Parent process
- Command line
- User

## Event ID 4689

- Process termination event.

---

# 11. Privilege Use Events

| Event ID | Description |
|----------|-------------|
| 4673 | Sensitive Privilege Used |
| 4674 | Operation on Privileged Object |

### Example

Sensitive privilege:

    SeDebugPrivilege

These events help monitor sensitive privileges and privileged operations.

---

# 12. Authentication - Kerberos / NTLM

| Event ID | Description |
|----------|-------------|
| 4768 | Kerberos TGT Request |
| 4769 | Kerberos Service Ticket Request |
| 4771 | Kerberos Pre-authentication Failed |
| 4776 | NTLM Authentication |

## SOC Detection

- Kerberos failures → Password spraying / brute force
- NTLM usage → Legacy authentication / potential abuse

---

# 13. Object Access Events

Track access to:

- Files
- Registry
- Other objects

| Event ID | Description |
|----------|-------------|
| 4656 | Handle Requested |
| 4663 | Object Access Attempt |
| 4658 | Handle Closed |

---

# 14. Policy & Audit Changes

| Event ID | Description |
|----------|-------------|
| 4719 | Audit Policy Changed |
| 4739 | Domain Policy Changed |

### SOC Risk

Attackers may disable auditing or modify policies to hide their activities.

---

# 15. Log Tampering

## Event ID 1102

    Security Log Cleared

### SOC Importance

- Attackers may clear security logs to remove evidence.
- Requires immediate investigation.

---

# 16. System & Security State Events

| Event ID | Description |
|----------|-------------|
| 4608 | Windows Started |
| 4609 | Windows Shutdown |
| 4616 | System Time Changed |

### SOC Detection

System time changes can indicate:

- Log manipulation
- Timeline manipulation

---

# 17. Security Event Detection Cheat Sheet

## Brute Force Attack

    Multiple 4625
    Failed Logon events
    from same IP/User

## Successful Attack

    4625
      ↓
    4624

## Privilege Escalation

    4624
      +
    4672
      +
    Group Membership Change

## Malware Execution

    4688
      ↓
    Suspicious Process / Command Line

## Persistence

    New Account 4720
      OR
    Service Creation 7045
      OR
    Scheduled Task

## Log Tampering

    1102
      ↓
    Security Log Cleared

---

# 18. Security Log Best Practices

- Always check Logon Type.
- Correlate multiple events.
- Investigate unusual logon times.
- Enable Advanced Audit Policy.
- Regularly review and monitor security logs.

---

# 19. System Logs

## What are System Logs?

System logs track:

- Operating System behavior
- Drivers
- Hardware
- Boot events

---

# 20. System Startup & Shutdown Events

| Event ID | Description |
|----------|-------------|
| 6005 | Event Log Service Started / System boot |
| 6006 | Event Log Service Stopped / Normal shutdown |
| 6008 | Unexpected Shutdown |
| 6013 | System Uptime |

---

# 21. Power & Reboot Events

| Event ID | Description |
|----------|-------------|
| 41 | Kernel-Power / Unexpected power failure, crash or BSOD |
| 1074 | Planned Shutdown/Restart initiated by user or process |
| 109 | Kernel Power Critical Error |

---

# 22. Driver & Hardware Events

| Event ID | Description |
|----------|-------------|
| 219 | Driver failed to load during system start |
| 225 | Device not migrated |
| 11 | Disk Controller Error |
| 15 | Device Not Ready |
| 7 | Bad Block Detected |

### SOC / Troubleshooting Use

These events help identify:

- Driver issues
- Hardware issues
- Disk problems
- System instability

---

# 23. Disk & Storage Events

| Event ID | Description |
|----------|-------------|
| 51 | Disk Warning |
| 55 | NTFS Corruption |
| 98 | NTFS Volume Corruption |

### SOC Use

Monitor for:

- Disk failures
- File-system corruption
- Storage problems

---

# 24. Service Control Manager Events

| Event ID | Description |
|----------|-------------|
| 7000 | Service Failed to Start |
| 7001 | Service Dependency Failed |
| 7009 | Service Timeout |
| 7011 | Service Timeout / No Response |
| 7034 | Service Crashed Unexpectedly |
| 7036 | Service State Changed |

### SOC Use

- Detect malicious service installation.
- Investigate unexpected service crashes.
- Detect service failures.

---

# 25. Network & Connectivity Events

| Event ID | Description |
|----------|-------------|
| 4201 | Network Adapter Connected |
| 4202 | Network Adapter Disconnected |
| 1014 | DNS Client Events |

### SOC Use

Monitor:

- Network adapter changes
- Connectivity issues
- DNS resolution failures

---

# 26. Time & System Integrity Events

| Event ID | Description |
|----------|-------------|
| 1 | Time Synchronized |
| 36 | Time Service Error |

### SOC Importance

Time changes/errors can affect event timelines and system integrity.

---

# 27. Crash & Error Reporting Events

| Event ID | Description |
|----------|-------------|
| 1000 | Application Error |
| 1001 | BugCheck / BSOD |

### Example

    System Crash
        ↓
    1001 BugCheck
        ↓
    BSOD Investigation

---

# 28. Critical System Health Indicators

High-priority events include:

| Event ID | Indicates |
|----------|-----------|
| 41 | Unexpected reboot / power issue |
| 6008 | Unexpected shutdown |
| 1001 | BSOD |
| 7, 11, 51, 55, 98 | Disk / file-system problems |
| 7000, 7034 | Service failure |
| 219, 225 | Driver issue |
| 1014 | DNS / network issue |

---

# 29. System Logs Cheat Sheet

    System Crash / Reboot
    → 41 + 6008 + 1001

    Disk Failure
    → 7 / 51 / 55 / 98

    Service Failure
    → 7000 / 7034

    Driver Issue
    → 219 / 225

    Network / DNS Issue
    → 1014

Use System Logs together with Security Logs for complete visibility of issues and attacks.

---

# 30. Application Logs

## What Do Application Logs Track?

- Application crashes
- Errors
- Software activity

### SOC Relevance

- Detect exploit attempts.
- Identify malicious application behavior.

### Example

    Application: Word crashed

    Possible:
    Exploit

A crash should be investigated in context.

---

# 31. Application Logs - Key Event IDs

## Application Start & General Events

| Event ID | Description |
|----------|-------------|
| 1000 | Application Error |
| 1001 | Application Hang |
| 1002 | Application Unresponsive |
| 1003 | Application Restart |
| 1004 | Application Start |
| 1005 | Application Stop |

---

# 32. Application Crash & Failure Events

| Event ID | Description |
|----------|-------------|
| 1006 | Application Crash |
| 1007 | Application Fault |

### .NET Runtime Events

| Event ID | Description |
|----------|-------------|
| 1026 | .NET Runtime Error |
| 1027 | .NET Runtime Warning |
| 1028 | .NET Runtime Information |
| 1029 | .NET Runtime Debug |

---

# 33. Application Install & Update Events

| Event ID | Description |
|----------|-------------|
| 1030 | Application Install |
| 1031 | Application Uninstall |
| 1032 | Application Update |
| 1033 | Configuration Change |
| 1034 | Configuration Error |

---

# 34. Security & Permission Events

| Event ID | Description |
|----------|-------------|
| 1040 | Application Access Denied |
| 1041 | Invalid Credentials |
| 1042 | Login Failure |
| 1043 | Permission Change |
| 1044 | Security Error |

---

# 35. Performance & Resource Events

| Event ID | Description |
|----------|-------------|
| 1050 | Application Performance Warning |
| 1051 | Application Performance Error |
| 1052 | Resource Warning |
| 1053 | Resource Error |
| 1054 | Timeout |

---

# 36. Application & System Integration Events

| Event ID | Description |
|----------|-------------|
| 1060 | Service Communication Failure |
| 1061 | External System Error |
| 1062 | Message Queue Error |
| 1063 | Email Send Failure |
| 1064 | API Call Failure |

---

# 37. Audit & Logging Events

| Event ID | Description |
|----------|-------------|
| 1070 | Audit Success |
| 1071 | Audit Failure |
| 1072 | Log Write Success |
| 1073 | Log Write Failure |

---

# 38. Important Application Event IDs

Quick reference:

    1000 → Application Error
    1001 → Application Hang
    1006 → Application Crash
    1026 → .NET Runtime Error
    1030 → Application Install
    1031 → Application Uninstall
    1032 → Application Update
    1033 → Configuration Change
    1040 → Access Denied
    1051 → Performance Error
    1060 → Service Communication Failure
    1072 → Log Write Success

### Monitoring

- Monitor Application Logs regularly.
- Detect crashes.
- Detect performance issues.
- Detect security problems.
- Detect integration failures early.

---

# 39. Windows Processes

## Definition

A process is a running instance of a program with its own:

- Memory space
- Threads
- Resources
- Security context

## Simple View

    Program on Disk
          ↓
       Executed
          ↓
    Process in Memory

### Example

    chrome.exe
        ↓
    Running
        ↓
    Process with PID

---

# 40. Key Components of a Process

## 1. PID - Process ID

- Unique identifier for a process.

Example:

    PID: 4321

## 2. Virtual Memory

- Each process gets isolated memory.

### SOC

- Process injection can abuse process memory.

## 3. Threads

- Units of execution inside a process.
- One process can contain multiple threads.

## 4. Handles

- References to system resources.

Examples:

- Files
- Registry
- Network

## 5. Security Context

- Process runs as a user/security context.

Examples:

- SYSTEM
- Administrator
- User

---

# 41. Windows Process Architecture

A process architecture shown in the PDF includes:

    System
        ↓
    smss.exe (master)
        ↓
    smss.exe (Session 0 / Session 1)
        ↓
    csrss.exe
    wininit.exe
        ↓
    services.exe
    lsass.exe
    lsaiso.exe
        ↓
    svchost.exe

Another user-session path:

    winlogon.exe
        ↓
    userinit.exe
        ↓
    explorer.exe

---

# 42. Process Life Cycle

    New
      ↓
    Ready
      ↓
    Running
      ↓
    Terminated

A process can also enter:

    Waiting

## New

- A new process is created to run a program.

## Ready

- Process is ready to run.

## Running

- Process is currently executing.

## Waiting

The process cannot run for various reasons.

It may wait for:

- User input
- Network
- Signal
- OS scheduling

## Terminated

- Process exits.

---

# 43. Windows Process Creation Flow

    1. User/System triggers execution
                ↓
    2. Win32 API called
                ↓
    3. Kernel creates process object
                ↓
    4. Memory allocated
                ↓
    5. Threads created
                ↓
    6. Process starts execution

---

# 44. Parent-Child Relationship

Every process is created by another process.

### Example

    explorer.exe
          ↓
      chrome.exe

- `explorer.exe` = Parent
- `chrome.exe` = Child

### SOC Insight

If the parent-child chain is abnormal:

    Suspicious

### Example

    winword.exe
         ↓
    powershell.exe

This can indicate suspicious execution.

---

# 45. Critical Windows System Processes

| Process | Function / Description | Importance |
|---------|-------------------------|------------|
| System / ntoskrnl.exe | Windows NT OS kernel; manages hardware, memory, processes and system resources | Critical |
| smss.exe | Session Manager Subsystem; starts user sessions and critical system processes | Critical |
| csrss.exe | Client/Server Runtime Subsystem; handles Win32 subsystem and console windows | Critical |
| wininit.exe | Windows initialization process; starts services and userinit.exe | Critical |
| services.exe | Service Control Manager; manages Windows services | Critical |
| lsass.exe | Local Security Authority; handles authentication, security policy and user logon | Critical |
| svchost.exe | Generic host process for Windows services | Critical |
| explorer.exe | Windows Explorer; manages desktop, taskbar, Start menu and file explorer | Important |
| spoolsv.exe | Print Spooler; manages print jobs and printer communication | Important |
| taskhostw.exe | Hosts tasks scheduled by user or system | Important |
| dwm.exe | Desktop Window Manager; provides visual effects and window management | Medium |
| svchost.exe (DNS Client) | Hosts DNS Client service; resolves domain names | Medium |
| svchost.exe (Power) | Hosts Power services; manages power settings | Medium |
| wuauclt.exe | Windows Update Client; checks for and installs updates | Low |
| MsMpEng.exe | Microsoft Defender Antivirus engine process | Low |

---

# 46. Critical Process Safety

## Warning

Do not terminate critical system processes unnecessarily.

Ending critical processes can cause:

- Data loss
- Complete OS failure
- System crash

## How to Identify Critical Processes

Check:

- Process file location
- Digital signature
- Process description
- Associated services
- Resource usage
- Process behavior

### Expected Location

    C:\Windows\System32
    C:\Windows

### Digital Signature

Verify:

    Microsoft Corporation

---

# 47. Process Monitoring Best Practices

- Regularly monitor system processes.
- Keep Windows and drivers updated.
- Use reputable security software.
- Investigate unknown/suspicious processes.
- Use Task Manager or Process Explorer for analysis.
- Always investigate before ending a system process.
- Create a system restore point before stopping a process if needed.

---

# 48. Windows Process Tree

## Standard Process Tree

    smss.exe
     ├── csrss.exe
     ├── wininit.exe
     ├── services.exe
     ├── lsass.exe
     └── svchost.exe

### SOC Use

Any unexpected deviation from the normal process relationship should be investigated.

### Example

    winword.exe
         ↓
      cmd.exe
         ↓
    powershell.exe

---

# 49. Process Types

## 1. User Processes

- Applications

## 2. System Processes

- Operating System-level processes

## 3. Background Processes

- Services

---

# 50. Process-Based Attacks

## 1. Process Injection

### Concept

Inject malicious code into another process.

### Example

    malware
       ↓
    inject
       ↓
    explorer.exe

### SOC Indicators

- Suspicious child processes
- Memory anomalies

---

# 51. DLL Injection

- Inject malicious DLL into another process.

---

# 52. Process Hollowing

### Concept

1. Start a legitimate process.
2. Replace its memory with malicious code.

### Example

    notepad.exe
         ↓
    Memory replaced
         ↓
       malware

The process may appear legitimate while executing malicious code.

---

# 53. LOLBins - Living Off the Land

## Concept

Using legitimate system tools for malicious activity.

Examples:

- powershell.exe
- cmd.exe
- rundll32.exe

### SOC Indicator

    powershell.exe
          ↓
    Encoded Command

---

# 54. Process Investigation Flow

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

---

# 55. Common Process Red Flags

Suspicious patterns:

- Word → PowerShell
- Browser → cmd.exe
- svchost.exe spawning child process
- Random executable from Temp folder

---

# 56. SOC Process Mindset

Do not ask only:

    "What is this process?"

Ask:

    "Why is this process running?"
    "Who started it?"
    "What did it do next?"

---

# 57. Windows Services

## Definition

A Windows Service is:

- A program that runs in the background.
- Runs without user interaction.
- Often starts automatically at system boot.

## Simple Understanding

    Application
        ↓
    Needs user
        ↓
    Visible

    Service
        ↓
    Runs silently
        ↓
    Background

---

# 58. Examples of Legitimate Services

- Windows Update
- Antivirus
- Print Spooler
- DHCP Client
- Remote Desktop Service

---

# 59. Service Control Manager (SCM)

## What is SCM?

SCM = Service Control Manager

It is the central controller of Windows services.

### Responsibilities

- Start services
- Stop services
- Manage service state
- Maintain service database

---

# 60. How Services Work Internally

The Service Control Manager communicates with:

- Windows Service Installer
- Windows Service Controller
- Windows Service Database
- Windows Services in Execution

### Architecture

    Windows Service Installer
              ↕
    Service Control Manager (SCM)
              ↕
    Windows Service Database

    Windows Service Controller
              ↕
    Service Control Manager

    Windows Services in Execution
              ↕
    Service Control Manager

---

# 61. Service Execution Flow

    System Boot
        ↓
    SCM starts
        ↓
    SCM reads Registry
        ↓
    Loads services
        ↓
    Services start running

---

# 62. Where Are Services Stored?

Services are stored in the Registry:

    HKLM\SYSTEM\CurrentControlSet\Services

Each service contains:

- Service Name
- Image Path
- Start Type
- Permissions

---

# 63. Service Types

## 1. Kernel Services

- Drivers

## 2. File System Services

- Disk operations

## 3. User-Mode Services

- Normal background services

---

# 64. Service Startup Types

| Type | Meaning |
|------|---------|
| Automatic | Starts at boot |
| Manual | Starts when needed |
| Disabled | Cannot start |

---

# 65. svchost.exe

## What is svchost.exe?

A container process that runs multiple services.

### Example

    svchost.exe
        ↓
    Multiple Services

### SOC Importance

- Malware may hide inside svchost.
- Can be difficult to detect.

---

# 66. Services vs Processes

| Feature | Process | Service |
|---------|---------|---------|
| User Interaction | Yes | No |
| Runs | On demand | Background |
| Persistence | No | Yes |

---

# 67. Common Service Attack Techniques

## 1. Malicious Service Installation

Example:

    Service Name:
    UpdateService

    Path:
    C:\Users\Temp\malware.exe

- Looks legitimate but is malware.

---

## 2. Service Hijacking

Replace the path of an existing service:

    legit.exe
        ↓
    replaced with
    malware.exe

---

## 3. Privilege Escalation via Services

If a service runs as:

    SYSTEM

then an attacker can get:

    Admin Access

---

## 4. Persistence

    Malware installs service
            ↓
    System Reboot
            ↓
    Service runs again

---

# 68. Real SOC Scenario

Observed logs:

    4624 → Login
        ↓
    4688 → powershell.exe
        ↓
    7045 → New service installed

### SOC Thinking

    Initial Access
          ↓
    Execution
          ↓
    Persistence

This combination should be investigated as a possible attack chain.

---

# 69. Service Investigation Flow

## SOC Steps

    1. Identify service
       Event ID 7045
                ↓
    2. Check path
                ↓
    3. Check user privileges
                ↓
    4. Check parent process
                ↓
    5. Check related logs
                ↓
    6. Correlate timeline

---

# 70. Service Red Flags

Suspicious indicators:

- New service created suddenly
- Service executable from Temp folder
- Random service name
- Service created after PowerShell

---

# 71. SOC Service Mindset

When you see a service, do not think:

    "This is just a background process."

Think:

    "Is this persistence?"
    "Is this privilege escalation?"
    "Is this attacker foothold?"

---

# 72. Complete Day 20 Investigation View

## Authentication

    4624 / 4625
         +
    User + IP + Logon Type
         ↓
    Investigate Login Pattern

## Process Execution

    4688
      ↓
    Process
      ↓
    Parent Process
      ↓
    Command Line
      ↓
    User Context
      ↓
    Network Activity
      ↓
    Correlate Logs

## Service Installation

    7045
      ↓
    New Service
      ↓
    Check Image Path
      ↓
    Check Privileges
      ↓
    Check Parent Process
      ↓
    Correlate Timeline

## Log Tampering

    1102
      ↓
    Security Log Cleared
      ↓
    Possible Evidence Removal
      ↓
    Investigate

---

# 73. Key Event IDs - Quick Reference

## Security Logs

| Event ID | Meaning |
|----------|---------|
| 4624 | Successful Logon |
| 4625 | Failed Logon |
| 4634 | Logoff |
| 4647 | User Initiated Logoff |
| 4648 | Explicit Credentials |
| 4672 | Special Privileges Assigned |
| 4720 | User Account Created |
| 4722 | Account Enabled |
| 4723 | Password Change Attempt |
| 4724 | Password Reset |
| 4725 | Account Disabled |
| 4726 | Account Deleted |
| 4728 | Added to Global Group |
| 4729 | Removed from Global Group |
| 4732 | Added to Local Group |
| 4733 | Removed from Local Group |
| 4756 | Added to Universal Group |
| 4757 | Removed from Universal Group |
| 4673 | Sensitive Privilege Used |
| 4674 | Privileged Object Operation |
| 4768 | Kerberos TGT Request |
| 4769 | Kerberos Service Ticket |
| 4771 | Kerberos Pre-auth Failed |
| 4776 | NTLM Authentication |
| 4656 | Handle Requested |
| 4663 | Object Access Attempt |
| 4658 | Handle Closed |
| 4719 | Audit Policy Changed |
| 4739 | Domain Policy Changed |
| 1102 | Security Log Cleared |
| 4608 | Windows Started |
| 4609 | Windows Shutdown |
| 4616 | System Time Changed |
| 4688 | Process Created |
| 4689 | Process Terminated |

---

# 74. System Log Event IDs

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
| 11 | Disk Controller Error |
| 15 | Device Not Ready |
| 7 | Bad Block Detected |
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
| 1014 | DNS Client Events |
| 1 | Time Synchronized |
| 36 | Time Service Error |
| 1000 | Application Error |
| 1001 | BugCheck / BSOD |
| 7045 | Service Installed |

---

# 75. Application Log Event IDs

| Event ID | Meaning |
|----------|---------|
| 1000 | Application Error |
| 1001 | Application Hang |
| 1002 | Application Unresponsive |
| 1003 | Application Restart |
| 1004 | Application Start |
| 1005 | Application Stop |
| 1006 | Application Crash |
| 1007 | Application Fault |
| 1026 | .NET Runtime Error |
| 1027 | .NET Runtime Warning |
| 1028 | .NET Runtime Information |
| 1029 | .NET Runtime Debug |
| 1030 | Application Install |
| 1031 | Application Uninstall |
| 1032 | Application Update |
| 1033 | Configuration Change |
| 1034 | Configuration Error |
| 1040 | Application Access Denied |
| 1041 | Invalid Credentials |
| 1042 | Login Failure |
| 1043 | Permission Change |
| 1044 | Security Error |
| 1050 | Performance Warning |
| 1051 | Performance Error |
| 1052 | Resource Warning |
| 1053 | Resource Error |
| 1054 | Timeout |
| 1060 | Service Communication Failure |
| 1061 | External System Error |
| 1062 | Message Queue Error |
| 1063 | Email Send Failure |
| 1064 | API Call Failure |
| 1070 | Audit Success |
| 1071 | Audit Failure |
| 1072 | Log Write Success |
| 1073 | Log Write Failure |

---

# 76. Final SOC Mindset

Windows logs tell the story of what happened.

A SOC Analyst should correlate:

    User
      +
    IP Address
      +
    Logon Type
      +
    Event ID
      +
    Process
      +
    Parent Process
      +
    Command Line
      +
    Service
      +
    Timeline

Do not investigate events in isolation.

Look for the complete attack chain.

---
| Event ID        | Meaning                  |
| --------------- | ------------------------ |
| **4624**        | Successful Logon         |
| **4625**        | Failed Logon             |
| **4648**        | Explicit Credentials     |
| **4672**        | Special Privileges       |
| **4688**        | Process Created ⭐        |
| **4720**        | User Account Created     |
| **4728 / 4732** | Group Member Added       |
| **4768 / 4769** | Kerberos authentication  |
| **4771**        | Kerberos Pre-auth Failed |
| **4776**        | NTLM Authentication      |
| **1102**        | Security Log Cleared ⭐   |
| **7045**        | Service Installed ⭐      |
