# Day 19 - Windows Architecture & Windows Registry

---

# Windows Architecture

## What is Windows Architecture?

Windows Architecture defines:

- How processes run
- How memory is handled
- How users authenticate
- How security is enforced

### SOC Relevance

Understanding Windows Architecture helps identify:

- Where attacks happen
- Which Windows components are involved

---

# Windows Architecture Layers

    User Mode
        ↓
    Kernel Mode
        ↓
    Hardware

## Ring Structure

    Ring 0 → Kernel Mode
    Ring 1 → Not Used
    Ring 2 → Not Used
    Ring 3 → User Mode

- Ring 0 = Most Privileged
- Ring 3 = Least Privileged

---

# User Mode

User Mode runs:

- Applications
- User processes
- Some services

### Examples

- Chrome
- Word
- User Applications

### Restrictions

- Cannot directly access hardware.
- Cannot directly modify the kernel.

### SOC Relevance

- Most malware starts in User Mode.

### Example

    Phishing
        ↓
    Word
        ↓
    PowerShell
        ↓
    Malicious Execution

---

# Kernel Mode

Kernel Mode runs:

- Windows Kernel
- Device Drivers
- Memory Manager

### Privilege

- Full system access.

### SOC Relevance

- Rootkits operate at this level.
- Kernel compromise can result in complete system control.

---

# Windows Architecture Components

## Windows Kernel

Handles:

- CPU Scheduling
- Interrupts
- Thread Execution

### SOC Insight

- The kernel is rarely directly attacked.
- If compromised, it can allow highly stealthy malware.

---

# Executive Layer

## Process Manager

- Creates and manages processes.

### SOC Relevance

Monitor for:

- Abnormal process spawning
- Suspicious process relationships

---

## Memory Manager

- Allocates and manages memory.

### SOC Relevance

- Fileless malware can operate in memory without requiring a traditional executable file on disk.

---

## I/O Manager

Handles:

- Disk activity
- Network activity

### SOC Relevance

Monitor for:

- Abnormal file activity
- Abnormal network activity

---

## Security Reference Monitor (SRM)

- Core Windows security component.
- Checks whether a user can access an object.

### SOC Use

Important when investigating:

- Privilege escalation
- Unauthorized access

---

# Hardware Abstraction Layer (HAL)

HAL = Hardware Abstraction Layer

- Interface between Operating System and Hardware.

    Operating System
           ↓
          HAL
           ↓
       Hardware

### SOC Relevance

- Used in advanced rootkits.

---

# Device Drivers

Device drivers allow Windows to communicate with hardware.

    Windows
       ↓
    Device Driver
       ↓
    Hardware

### Security Threats

- Vulnerable drivers can lead to privilege escalation.
- Signed driver abuse can be used by attackers.

---

# Windows Process Architecture

## What is a Windows Process?

A process is an executing instance of a program.

A process acts as a container for resources such as:

- Memory
- Handles
- Threads

Each process has a unique:

- PID = Process Identifier

### Process Contains

- PID
- Memory
- Threads

---

# Must-Know Windows System Processes

## smss.exe

- First user-mode process.

## wininit.exe

- Starts the system.

## services.exe

- Manages Windows services.

## lsass.exe

LSASS = Local Security Authority Subsystem Service

Handles:

- Authentication
- Credential storage

### Attack

- Attackers may use Mimikatz to dump credentials.

    Mimikatz
        ↓
    Credential Dumping

## svchost.exe

- Hosts Windows services.

### SOC Relevance

- Malware may attempt to hide or execute through service-hosting processes.

---

# SOC Process Detection Example

    winword.exe
         ↓
    powershell.exe
         ↓
       cmd.exe

### Possible Activity

- Malicious Macro Execution

---

# Windows Memory Architecture

## Virtual Memory

- Each process gets isolated memory.

    Process 1 → Isolated Memory
    Process 2 → Isolated Memory
    Process 3 → Isolated Memory

### SOC Threats

- Process Injection
- DLL Injection
- Fileless Malware

---

# Windows Authentication Flow

    User Login
        ↓
      LSASS
        ↓
    Authentication
        ↓
    Access Token

---

# Access Token

An Access Token contains:

- User Identity
- User Privileges

It determines what the authenticated user is allowed to access.

### SOC Use

    Token Theft
        ↓
    Privilege Escalation

---

# Windows Registry

## What is Windows Registry?

Windows Registry is a central database that stores:

- System Configuration
- User Settings
- Application Data

---

# Registry Structure

    Hive
      ↓
    Key
      ↓
    Subkey
      ↓
    Value

---

# Root Keys / Hives

| Hive | Meaning |
|------|---------|
| HKLM | System-wide |
| HKCU | Current user |
| HKCR | File associations |
| HKU | All users |
| HKCC | Hardware configuration |

---

# How Registry Works

## When System Boots

    1. Windows reads Registry
    2. Loads configurations
    3. Starts services
    4. Applies user settings

## When an Application Runs

    Application
         ↓
    Reads Registry
         ↓
    Loads Configuration

---

# Registry Value Types

| Type | Meaning |
|------|---------|
| REG_SZ | String |
| REG_DWORD | Numbers |
| REG_BINARY | Binary |

---

# Registry & Attacks

## Run Key Persistence

### Location

`HKCU\Software\Microsoft\Windows\CurrentVersion\Run`

### Attack

- Malware adds an executable such as `malware.exe` to the Run key.

### Result

    User Login
        ↓
    Run Key
        ↓
    malware.exe
        ↓
    Execution

- Malware runs automatically at every login.

---

# RunOnce Key

- Executes a program once.
- Can be abused by malware.

---

# Services Registry Persistence

### Location

`HKLM\SYSTEM\CurrentControlSet\Services`

### Attack

- Attackers can install malware as a Windows service.

---

# WMI Persistence

- Advanced persistence technique.
- Uses Windows Management Instrumentation.

---

# Registry Hijacking

Attackers can:

    Replace legitimate path
            ↓
      Malicious path

- This can cause a legitimate action to execute malicious code.

---

# SOC Detection

## What to Monitor

### Suspicious Registry Entries

Example:

`powershell.exe`

inside a Run key.

### Unknown Executables

Example:

`random.exe`

configured to auto-start.

### Unusual Paths

Example:

`AppData\Temp\`

---

# Registry Forensics

Registry can help extract:

- Installed Software
- User Activity
- Execution History

---

# Windows Architecture + Registry Attack Flow

    Phishing
        ↓
      Word
        ↓
    PowerShell
        ↓
    Payload Executes
        ↓
    Registry Run Key Modified
        ↓
    Persistence Achieved
        ↓
    LSASS Attacked
        ↓
    Lateral Movement

---

# Registry - Event ID 4657

## Event ID

`4657`

### Meaning

- Registry Key Modified

### Example

Key:

`HKCU\...\Run`

Value:

`malware.exe`

### SOC Result

- Persistence Detected

---

# Real SOC Example

    Event ID 4657
           ↓
    Registry Key Modified
           ↓
    HKCU\...\Run
           ↓
    malware.exe
           ↓
    Persistence Detected

---

# Final SOC Mindset

When analyzing a Windows system, ask:

1. Which process ran?
2. What did it modify?
3. Any Registry persistence?
4. Any credential access?
5. Any lateral movement?

---

# Day 19 - Key Points

    User Mode
    → Applications + User Processes

    Kernel Mode
    → Kernel + Drivers + Memory Manager
    → Full System Access

    Process
    → Running program
    → PID + Memory + Threads

    lsass.exe
    → Authentication + Credential Storage

    Memory Threats
    → Process Injection
    → DLL Injection
    → Fileless Malware

    Authentication
    → User Login → LSASS → Authentication → Access Token

    Access Token
    → User Identity + Privileges

    Registry
    → System Configuration + User Settings + Application Data

    Registry Structure
    → Hive → Key → Subkey → Value

    Run Key
    → Common Persistence Location

    Event ID 4657
    → Registry Key Modified

    SOC Investigation
    → Process → Modification → Persistence → Credentials → Lateral Movement

---
