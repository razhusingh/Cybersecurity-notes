
## DAY 19 — WINDOWS ARCHITECTURE + WINDOWS REGISTRY
.

---

# ⚡ 1. 30-SECOND RECALL

Windows Architecture explains:
`Processes + Memory + Authentication + Security`

### Two Modes
- **User Mode** → applications/user processes; restricted
- **Kernel Mode** → kernel/drivers; full system access

`User Mode → Executive → Kernel → HAL → Drivers → Hardware`

### Important Windows Components
- **Kernel** → CPU scheduling, interrupts, thread execution
- **Process Manager** → creates processes
- **Memory Manager** → allocates memory
- **I/O Manager** → disk + network I/O
- **SRM** → security/access checks
- **HAL** → OS ↔ hardware
- **Drivers** → hardware communication

### Important Processes
`smss.exe → wininit.exe → services.exe`
`lsass.exe → authentication + credentials`
`svchost.exe → hosts services`

### Authentication
`User Login → LSASS → Authentication → Access Token`

### Registry
`Hive → Key → Subkey → Value`

### Main Attack Story
`Phishing → Word → PowerShell → Payload → Registry Persistence → LSASS → Lateral Movement`

---

# 🧠 2. MUST REMEMBER

## A. WINDOWS USER MODE vs KERNEL MODE

| User Mode | Kernel Mode |
|---|---|
| Applications/user processes | Kernel + drivers |
| Restricted access | Full system access |
| Cannot directly access hardware | Can access hardware |
| Cannot modify kernel | Can control kernel |
| Most malware starts here | Rootkits may operate here |

**SOC:** Kernel compromise can mean complete system control.

---

## B. WINDOWS KERNEL

Handles:
- CPU scheduling
- Interrupts
- Thread execution

**SOC:** Kernel compromise may enable stealth malware.

---

## C. EXECUTIVE LAYER

### Process Manager
- Creates processes
- SOC → detect abnormal process spawning

### Memory Manager
- Allocates memory
- SOC → fileless malware can operate in memory

### I/O Manager
- Handles disk + network I/O
- SOC → investigate abnormal file/network activity

### Security Reference Monitor (SRM)
- Core security engine
- Checks whether a user can access an object
- SOC → privilege escalation / unauthorized access

---

## D. HAL + DEVICE DRIVERS

### HAL
**Hardware Abstraction Layer**
- Interface between OS and hardware
- Relevant to advanced rootkits

### Device Drivers
- Communicate with hardware
- Vulnerable drivers → privilege escalation
- Signed-driver abuse can be a threat

---

# 🖥️ 3. WINDOWS PROCESS ARCHITECTURE

A process = **executing/running instance of a program**.

Contains:
- PID
- Memory
- Threads
- Handles/resources

**PID = Process Identifier**

---

## MUST-KNOW SYSTEM PROCESSES

| Process | Function |
|---|---|
| `smss.exe` | First user-mode process |
| `wininit.exe` | Starts system |
| `services.exe` | Manages services |
| `lsass.exe` | Authentication + credential storage |
| `svchost.exe` | Hosts services |

---

## 🔥 LSASS

**Functions:**
- Authentication
- Credential storage

**Attack:**
- Mimikatz → credential dumping

**SOC indicator:**
`Unexpected LSASS access → investigate credential dumping`

---

## ⚠️ svchost.exe

- Hosts Windows services
- Malware may hide/abuse service-hosting processes

**Never decide maliciousness from process name alone.**

Check:
- Parent process
- Command line
- File path
- Network activity
- Associated service

---

# 🚨 4. SUSPICIOUS PROCESS CHAIN

`winword.exe → powershell.exe → cmd.exe`

Possible:
`Malicious Word Macro → PowerShell → Command Execution`

### SOC Investigation
Check:
- Parent process
- Child process
- Command line
- Resulting activity

**Memory trigger:**
`PARENT → CHILD → COMMAND → ACTIVITY`

---

# 🧠 5. WINDOWS MEMORY ARCHITECTURE

## Virtual Memory
Each process gets **isolated memory**.

### Important Threats

**Process Injection**
- Malicious code inserted into another process

**DLL Injection**
- Malicious DLL loaded into another process

**Fileless Malware**
- Malware operating mainly in memory

---

# 🔐 6. WINDOWS AUTHENTICATION

### Flow

`User Login → LSASS → Authentication → Access Token`

### Access Token Contains
- User identity
- Privileges

### SOC Threat
`Token Theft → Privilege Escalation`

---

# 🗂️ 7. WINDOWS REGISTRY

Registry = **central database** storing:

- System configuration
- User settings
- Application data

### Structure

`Hive → Key → Subkey → Value`

---

# 🏠 8. REGISTRY HIVES

| Hive | Meaning |
|---|---|
| `HKLM` | System-wide |
| `HKCU` | Current user |
| `HKCR` | File associations |
| `HKU` | All users |
| `HKCC` | Hardware configuration |

### Memory
- **LM** → Local Machine
- **CU** → Current User
- **CR** → Classes/File associations
- **U** → Users
- **CC** → Current Configuration

---

# ⚙️ 9. HOW REGISTRY WORKS

## System Boot

`Windows reads Registry`
→ `Loads configurations`
→ `Starts services`
→ `Applies user settings`

## Application

`Application → Reads Registry → Loads configuration`

---

# 🔢 10. REGISTRY VALUE TYPES

- `REG_SZ` → String
- `REG_DWORD` → Number
- `REG_BINARY` → Binary

---

# 🚨 11. REGISTRY ATTACKS

## 1. RUN KEY PERSISTENCE

Location:

`HKCU\Software\Microsoft\Windows\CurrentVersion\Run`

Attack:

`malware.exe added → executes at every login`

### SOC Indicators
- `powershell.exe` in Run key
- Unknown executable
- Random executable name
- Unusual path
- `AppData\Temp\`

---

## 2. RUNONCE

- Executes once
- Can be abused by malware

---

## 3. SERVICES PERSISTENCE

Location:

`HKLM\SYSTEM\CurrentControlSet\Services`

Attack:

`Malware → Installs as Windows Service → Persistence`

---

## 4. WMI PERSISTENCE

- Advanced persistence technique

---

## 5. REGISTRY HIJACKING

- Replace legitimate Registry path with attacker-controlled path

---

# 🔎 12. SOC REGISTRY DETECTION

### Monitor For
- Suspicious Registry entries
- PowerShell in Run key
- Unknown executables
- Random auto-start programs
- Unusual executable paths
- `AppData\Temp\`

### 🔥 EVENT ID 4657

**4657 → Registry Key Modified**

Example:

`HKCU\...\Run → malware.exe`

→ **Persistence detected**

---

# 🕵️ 13. REGISTRY FORENSICS

Registry can provide evidence about:

- Installed software
- User activity
- Execution history

---

# 🔥 14. COMPLETE WINDOWS ATTACK FLOW

`Phishing`
↓
`Word`
↓
`PowerShell`
↓
`Payload Executes`
↓
`Registry Run Key Modified`
↓
`Persistence Achieved`
↓
`LSASS Attacked`
↓
`Lateral Movement`

### Attack Mapping

| Activity | Stage |
|---|---|
| Phishing | Initial Access |
| Word → PowerShell | Execution |
| Registry Run Key | Persistence |
| LSASS | Credential Access |
| Lateral Movement | Movement to other systems |

---

# 🎯 15. SOC ANALYST MINDSET

When analyzing a Windows alert, ask:

1. **Which process ran?**
2. **What did it modify?**
3. **Any Registry persistence?**
4. **Any credential access?**
5. **Any lateral movement?**

### Don't Investigate in Isolation

Instead connect:

`Process → Modification → Persistence → Credential Access → Lateral Movement`

### Core Memory Trigger

`PROCESS → MODIFY → PERSIST → CREDENTIALS → MOVE`

---

# 🎤 16. INTERVIEW Q&A

### Q1. What is Windows Architecture?
**A:** The structure defining how Windows handles processes, memory, authentication and security.

### Q2. User Mode vs Kernel Mode?
**A:** User Mode is restricted; Kernel Mode has full system access.

### Q3. What does LSASS do?
**A:** Handles authentication and credential storage.

### Q4. Why is `svchost.exe` important in investigation?
**A:** It hosts services and can be abused by malware; process context must be checked.

### Q5. What is Virtual Memory?
**A:** Each process gets isolated memory.

### Q6. What is an Access Token?
**A:** It contains user identity and privileges.

### Q7. What is Windows Registry?
**A:** A central database storing system configuration, user settings and application data.

### Q8. What is Run Key persistence?
**A:** Adding an executable to the Run key so it executes at login.

### Q9. What does Event ID 4657 indicate?
**A:** Registry Key Modified.

### Q10. What is Registry Hijacking?
**A:** Replacing a legitimate Registry path with an attacker-controlled path.

### Q11. What can Registry forensics reveal?
**A:** Installed software, user activity and execution history.

### Q12. Why is `winword.exe → powershell.exe → cmd.exe` suspicious?
**A:** It may indicate malicious macro → PowerShell → command execution.

---

# 📝 17. QUESTION PAPER MODE
## QUESTIONS ONLY

1. What is Windows Architecture?
2. Differentiate User Mode and Kernel Mode.
3. What are the functions of the Kernel, Process Manager, Memory Manager and I/O Manager?
4. What is the role of SRM?
5. What are HAL and Device Drivers?
6. What is a Windows process and what does a PID identify?
7. What are the functions of `smss.exe`, `wininit.exe`, `services.exe`, `lsass.exe` and `svchost.exe`?
8. Why is `winword.exe → powershell.exe → cmd.exe` suspicious?
9. What is Virtual Memory? Name three related attack techniques.
10. Explain the Windows authentication flow and Access Token.
11. What is Windows Registry and what is its hierarchy?
12. Explain HKLM, HKCU, HKCR, HKU and HKCC.
13. What are REG_SZ, REG_DWORD and REG_BINARY?
14. What is Run Key persistence? Give its Registry path.
15. Explain RunOnce, Services Persistence, WMI Persistence and Registry Hijacking.
16. What Registry indicators should a SOC analyst monitor?
17. What does Event ID 4657 indicate?
18. What information can Registry forensics provide?
19. Explain the complete Phishing → Registry Persistence → LSASS → Lateral Movement attack flow.
20. What five questions should a SOC analyst ask when investigating a Windows alert?

---

# 🔑 18. ANSWER KEY

1. Structure defining Windows process, memory, authentication and security handling.
2. User Mode is restricted; Kernel Mode has full system access.
3. Kernel → CPU scheduling/interrupts/threads; Process Manager → processes; Memory Manager → memory; I/O Manager → disk/network I/O.
4. Security Reference Monitor performs security/access checks.
5. HAL interfaces OS with hardware; drivers communicate with hardware.
6. A process is a running program; PID uniquely identifies it.
7. `smss.exe` → first user-mode process; `wininit.exe` → starts system; `services.exe` → manages services; `lsass.exe` → authentication/credentials; `svchost.exe` → hosts services.
8. It may indicate malicious Word macro → PowerShell → command execution.
9. Isolated process memory; Process Injection, DLL Injection and Fileless Malware.
10. `User Login → LSASS → Authentication → Access Token`; token contains identity and privileges.
11. Central database; `Hive → Key → Subkey → Value`.
12. HKLM → system-wide; HKCU → current user; HKCR → file associations; HKU → all users; HKCC → hardware configuration.
13. String, number and binary.
14. Adding an executable to the Run key for execution at login; `HKCU\Software\Microsoft\Windows\CurrentVersion\Run`.
15. RunOnce → one-time execution; Services → malware installs as service; WMI → advanced persistence; Registry Hijacking → attacker-controlled replacement path.
16. Suspicious entries, PowerShell, unknown/random executables, auto-start entries and unusual paths such as `AppData\Temp\`.
17. Registry Key Modified.
18. Installed software, user activity and execution history.
19. `Phishing → Word → PowerShell → Payload → Run Key → Persistence → LSASS → Lateral Movement`.
20. Which process ran? What did it modify? Any Registry persistence? Any credential access? Any lateral movement?

---

# 🧠 19. FINAL MEMORY MAP

### WINDOWS
`MODE → PROCESS → MEMORY → LSASS → TOKEN`

### REGISTRY
`HIVE → KEY → SUBKEY → VALUE`

### PERSISTENCE
`RUN → RUNONCE → SERVICE → WMI`

### INVESTIGATION
`PROCESS → MODIFY → PERSIST → CREDENTIALS → MOVE`

### ATTACK STORY
`PHISHING → EXECUTION → PERSISTENCE → CREDENTIAL ACCESS → LATERAL MOVEMENT`

---
