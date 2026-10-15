# Class 35 — Malware Analysis

# 1. Malware Analysis

## What Is Malware Analysis?

Malware analysis is the process of examining malicious software to understand its:

- Behaviour
- Origin
- Architecture
- Threat indicators

During an incident, a malware analyst tries to answer four questions:

1. What happened?
2. How did it get in?
3. What can it do?
4. How do we detect or stop it?

## Important Definitions

### Malware
Malicious software is code designed to fulfil an attacker's objective, such as:

- Stealing sensitive data
- Disrupting services
- Demanding money through extortion
- Conducting espionage

### Malware Analysis
Malware analysis involves examining software to identify:

- **IOCs (Indicators of Compromise):** IP addresses, domains, registry keys, and file hashes associated with suspicious activity.
- **TTPs (Tactics, Techniques, and Procedures):** Methods and procedures used by attackers.

These findings help security teams update their defences.

# 2. Taxonomy of Malware Types

Different malware types have different mechanisms and objectives.

| Malware Type | Core Mechanism | Objective |
|---|---|---|
| Ransomware | Encrypts local or network files using asymmetric key cryptography. | Extorts victims for decryption keys. |
| RAT (Remote Access Trojan) | Establishes an interactive, encrypted Command and Control (C2) channel. | Enables remote control, keylogging, and shell access. |
| InfoStealer | Scrapes browser SQLite databases, cryptocurrency wallets, and system credentials. | Steals sensitive credentials for sale or initial access. |
| Worm | Exploits network vulnerabilities to spread automatically. | Spreads rapidly without human interaction across flat networks. |
| Rootkit | Operates at the kernel level (Ring 0) or hypervisor level. | Hooks OS API calls to hide processes, files, and network sockets. |
| Botnet Client | Joins an infected host to a centralised network overlay. | Executes coordinated tasks such as DDoS or mass spam distribution. |

## Quick Understanding

- **Ransomware:** Encrypts files and demands payment for decryption.
- **RAT:** Gives an attacker remote access to a compromised system.
- **InfoStealer:** Steals credentials and other sensitive information.
- **Worm:** Spreads automatically by exploiting network vulnerabilities.
- **Rootkit:** Hides processes, files, or network sockets.
- **Botnet Client:** Connects an infected system to a network used for coordinated activities.

# 3. Binary Malware vs. Script-Based Malware

Malware executables can be divided into two broad categories.

## 3.1 Binary Malware

### Characteristics
- Contains native machine code.
- Is architecture-bound.
- Requires assembly analysis or reverse engineering.
- Examples: `.exe`, `.dll`, `.sys`, and ELF files.

### Execution
Binary malware is compiled into native CPU instructions, such as x86/x64 machine code. It interacts with system APIs through the OS loader.

### Analysis Approach
Binary analysis can involve:

- Disassembly using IDA Pro or Ghidra.
- Debugging using x64dbg.
- Reading assembly instructions such as `mov`, `push`, and `call`.

### Common Delivery Methods
Binary malware may arrive through:

- Email attachments, such as `invoice.pdf.exe`.
- Malicious downloads.
- Removable media.
- Another infection.

Attackers may disguise executables using misleading icons or by hiding the real file extension.

### Identifying Binary Malware
A checksum can help identify an executable.

For example, `md5sum` calculates an MD5 checksum of a file. The checksum can help identify the file even if its name or extension changes.

Binary files may also contain hardcoded strings or byte sequences used as unique identifiers by antivirus and detection engines.

## 3.2 Script-Based Malware

### Characteristics
- Written in high-level scripting languages.
- Runs through interpreters available on the operating system.
- May use heavy obfuscation.
- Examples: `.ps1`, `.vbs`, `.js`, `.bat`, and `.py`.

### Execution
Script-based malware relies on interpreters already present on the system, such as:

- `powershell.exe`
- `wscript.exe`

### Analysis Approach
Analysis may involve deobfuscating the script by:

- Resolving string concatenation.
- Decoding Base64.
- Examining XOR loops.
- Understanding renamed variables.

### Common Delivery Methods
Script-based malware may arrive through:

- Email attachments.
- Office documents containing macros.
- Malicious websites.

Example:

A user opens an email attachment named `report.docm`. The document contains a macro that runs a hidden PowerShell script.

Scripts may also be used for initial access and can execute code directly in memory without writing files to disk.

## 3.3 Binary vs. Script Malware — Comparison

| Feature | Binary Malware | Script-Based Malware |
|---|---|---|
| Form | Compiled executable | Script file |
| Code | Native machine instructions | High-level interpreted code |
| Execution | Uses the OS loader and system APIs | Uses an operating-system interpreter |
| Examples | `.exe`, `.dll`, `.sys`, ELF | `.ps1`, `.vbs`, `.js`, `.bat`, `.py` |
| Analysis | Disassembly and debugging | Deobfuscation and script analysis |
| Example tools | IDA Pro, Ghidra, x64dbg | Analysis may involve resolving encoded or obfuscated script content |

# 4. High-Profile Real-World Cases

## 4.1 Stuxnet (2010)

- Described as the first known cyber weapon targeting physical infrastructure.
- Used four zero-day vulnerabilities.
- Hijacked Siemens PLCs controlling Iranian nuclear centrifuges.
- Faked normal telemetry data.

## 4.2 WannaCry (2017)

- A global ransomware outbreak.
- Used the NSA's leaked EternalBlue exploit targeting SMBv1.
- Spread autonomously as a worm.
- Caused widespread disruption to critical infrastructure, including the UK's NHS.

## 4.3 SolarWinds / SUNBURST (2020)

- A sophisticated supply-chain attack.
- State-sponsored threat actors injected a backdoor into Orion software updates.
- Compromised thousands of government and corporate networks globally.

# 5. Malware Analysis Methodologies

The malware analysis pipeline includes three approaches:

1. Static Analysis
2. Dynamic Analysis
3. Code Reversing

## 5.1 Static Analysis

### Definition
Static analysis examines a malware sample without executing its code.

The analyst examines the file's properties while it is not running.

### What Can Be Examined?
- File hashes.
- Embedded strings.
- PE header information.
- PE file sections.
- Compiler metadata.
- YARA signatures.
- Import Address Table.
- Code through a disassembler.

For a malicious document, examining its properties without running it is also static analysis.

### Example Tools
- PEStudio
- FLOSS
- pestr
- YARA

### Important Points
Static analysis can reveal important information about malware. However, it may not be sufficient when malware hides its properties to prevent analysis.

## 5.2 Dynamic Analysis

### Definition
Dynamic analysis involves running a malware sample in a monitored, isolated environment to observe its actual behaviour.

This can be done manually in a virtual machine with monitoring tools or automatically in a sandbox.

### What Can Be Observed?
- Process creation trees.
- Network callbacks, including IP and DNS activity.
- File creation or dropping.
- Registry persistence.
- API calls.
- File-system activity.
- Memory dumps.

### Example Tools
- ProcMon (Process Monitor)
- Wireshark
- x64dbg
- CAPE V2 Sandbox

### Important Points
- Malware can hide its properties during static analysis.
- Dynamic analysis may reveal behaviours that static analysis does not.
- A controlled environment allows the analyst to observe malware activity.

## 5.3 Code Reversing

Code reversing involves examining compiled code to understand its structure and behaviour.

The methodology diagram identifies:

- **Assembly (x86):** Examining machine instructions in assembly form.
- **IDA Pro / Ghidra:** Tools for examining compiled code.
- **x64dbg Debugging:** Examining execution using a debugger.
- **API Hook Breaking:** An activity listed in the analysis pipeline.

## 5.4 Analysis Methodologies — Comparison

| Feature | Static Analysis | Dynamic Analysis | Code Reversing |
|---|---|---|---|
| Main approach | Examine without executing | Run in an isolated, monitored environment | Examine compiled code and its instructions |
| Examples of activities | Hashes, strings, PE headers, YARA signatures | Process trees, network traffic, files, registry, API calls, memory dumps | Assembly analysis and debugging |
| Tools shown | PEStudio, FLOSS, pestr, YARA | ProcMon, Wireshark, x64dbg, CAPE V2 Sandbox | IDA Pro, Ghidra, x64dbg |

# 6. Anti-Analysis Techniques and Evasion

Attackers use techniques to make malware analysis and reverse engineering more difficult.

## 6.1 Anti-Debugging

### Purpose
Anti-debugging techniques attempt to detect whether malware is running under a debugger.

### Techniques
- Checking execution flags through Windows APIs such as `IsDebuggerPresent()`.
- Reading the `BeingDebugged` flag in the PEB (Process Environment Block).

### Bypass Methods Listed
- Patching a conditional branch instruction, such as `JZ` or `JNZ`, in a debugger.
- Using plugins such as ScyllaHide.

## 6.2 Anti-VM / Sandbox Evasion

### Purpose
Malware may attempt to detect whether it is running inside a virtual machine or sandbox.

### Detection Techniques
- Checking for VMware or VirtualBox drivers.
- Checking registry keys.
- Checking MAC address prefixes.
- Checking for low CPU core counts.

### RDTSC
`RDTSC` stands for Read Time-Stamp Counter.

Malware can use this instruction to calculate execution-time differences. Debuggers and sandboxes may introduce measurable latency.

## 6.3 Packing and Obfuscation

### Packing
Packing involves compressing or encrypting the original payload on disk.

### Examples
- UPX
- Custom crypters

### Execution Process
1. The packed file is stored on disk.
2. At runtime, the file uncompresses itself into memory.
3. Execution then jumps to the OEP (Original Entry Point).

# 7. Essential Tools for a Malware Analysis Lab

| Category | Tools | Primary Purpose |
|---|---|---|
| Static Inspection | CFF Explorer, PEStudio, Detect It Easy (DiE) | Inspect PE structures, dependencies, sections, and signatures. |
| Disassemblers | IDA Free, Ghidra, Cutter | Transform machine code into readable assembly or decompiled C-like code. |
| Dynamic Debuggers | x64dbg, x32dbg, WinDbg | Control execution step by step, set breakpoints, and dump memory. |
| System Monitoring | Process Monitor (ProcMon), Process Hacker | Track real-time file-system, registry, process, and thread activities. |
| Network Interception | Wireshark, Fiddler, PolarProxy | Capture, inspect, and decrypt C2 network communication packets. |

## Tool Categories — Quick Recall

- **Static inspection:** Examines executable structures and signatures.
- **Disassemblers:** Convert machine code into readable assembly or decompiled code.
- **Dynamic debuggers:** Control program execution, set breakpoints, and dump memory.
- **System monitoring:** Tracks file-system, registry, process, and thread activities.
- **Network interception:** Captures and inspects network communications.

# 8. SOC Analyst L1 — Practical Understanding

When malware is involved in an incident, the analysis concepts in this class help answer four questions:

1. What happened?
2. How did the malware enter the system?
3. What can the malware do?
4. How can it be detected or stopped?

Important concepts to recognise:

- **IOCs:** IP addresses, domains, registry keys, and file hashes.
- **TTPs:** Attacker tactics, techniques, and procedures.
- **Static analysis:** Examining the sample without executing it.
- **Dynamic analysis:** Observing the sample in a monitored, isolated environment.
- **Anti-analysis:** Techniques used to hinder reverse engineering.
- **Malware categories:** Understand the mechanism and objective of each type.
- **Analysis tools:** Know the purpose of each tool category.

# 9. Quick Revision Table

| Term | Meaning |
|---|---|
| Malware | Software designed to fulfil an adversary's objective |
| Malware Analysis | Examination of malware to understand behaviour and identify indicators |
| IOC | Indicator of Compromise |
| TTP | Tactics, Techniques, and Procedures |
| C2 | Command and Control |
| RAT | Remote Access Trojan |
| PE | Portable Executable |
| Static Analysis | Examining a sample without executing it |
| Dynamic Analysis | Running a sample in an isolated, monitored environment |
| PEB | Process Environment Block |
| RDTSC | Read Time-Stamp Counter |
| OEP | Original Entry Point |
| YARA | Tool listed for scanning malware signatures |
| ProcMon | Process Monitor |
| DDoS | Distributed Denial of Service |
