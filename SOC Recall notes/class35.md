# Class 35 — Malware Analysis

### 1. 30-Second Recall

- **Malware:** Software designed to steal data, damage systems, or perform malicious activities.
- **Malware Analysis:** Studying malware to understand what it does and how to detect or stop it.
- **IOC:** A clue that may indicate a security incident, such as a suspicious IP address or file hash.
- **TTPs:** Methods attackers use to carry out their activities.
- **Static Analysis:** Examine malware without running it.
- **Dynamic Analysis:** Run malware in an isolated environment and observe its behaviour.
- **Code Reversing:** Examine compiled code to understand how it works.
- **Anti-Analysis:** Techniques malware uses to make investigation difficult.

### 2. Must Remember

#### A. Six Types of Malware

| Malware | Easy Meaning |
|---|---|
| Ransomware | Encrypts files and demands payment for decryption. |
| RAT | Allows an attacker to control a computer remotely. |
| InfoStealer | Steals passwords and sensitive information. |
| Worm | Spreads automatically by exploiting network vulnerabilities. |
| Rootkit | Hides processes, files, and network activity. |
| Botnet Client | Connects an infected computer to a network controlled by an attacker. |

#### B. Binary vs. Script Malware

**Binary Malware**
- Compiled machine code.
- Examples: `.exe`, `.dll`, `.sys`, ELF.
- Runs through the operating system's loader and interacts with system APIs.
- May use misleading icons or hidden file extensions.
- Can contain hardcoded strings or byte patterns that help identify it.
- `md5sum` calculates an MD5 hash that can help identify a file.
- Analysis tools: IDA Pro, Ghidra, x64dbg.

**Script-Based Malware**
- Runs through an interpreter.
- Examples: `.ps1`, `.vbs`, `.js`, `.bat`, `.py`.
- May arrive through email attachments, Office macros, or malicious websites.
- May run code directly in memory without writing files to disk.
- Analysis may involve Base64 decoding, resolving string concatenation, examining XOR loops, and understanding renamed variables.

**Remember:** Binary = compiled code. Script = code run through an interpreter.

#### C. Three Malware Analysis Methods

| Method | Meaning | Tools |
|---|---|---|
| Static Analysis | Examine malware without running it. | PEStudio, FLOSS, pestr, YARA |
| Dynamic Analysis | Run malware in an isolated environment and observe it. | ProcMon, Wireshark, x64dbg, CAPE V2 |
| Code Reversing | Examine compiled code and assembly to understand how it works. | IDA Pro, Ghidra, x64dbg |

**Static Analysis — Remember**
- File hashes and embedded strings.
- PE headers and sections.
- Compiler metadata.
- Import Address Table (IAT).
- YARA signatures.
- Disassembly without executing the sample.

**Dynamic Analysis — Remember**
- Process creation trees.
- Network callbacks (IP/DNS) and PCAP traffic.
- File creation or dropping.
- Registry persistence.
- API calls and memory dumps.
- Can be performed in a virtual machine or sandbox.

**Code Reversing — Remember**
- Assembly instructions: `mov`, `push`, `call`.
- Examining compiled code with IDA Pro or Ghidra.
- Debugging with x64dbg.
- API Hook Breaking is listed in the class methodology diagram.

#### D. Anti-Analysis Techniques

**1. Anti-Debugging**
- Malware tries to detect whether a debugger is present.
- `IsDebuggerPresent()` is a Windows API used for debugger detection.
- The PEB (Process Environment Block) contains the `BeingDebugged` flag.
- The PDF lists conditional-branch patching (`JZ`/`JNZ`) and ScyllaHide as bypass methods.

**2. Anti-VM / Sandbox Evasion**
Malware may check for:
- VMware or VirtualBox drivers.
- Registry keys.
- MAC address prefixes.
- Low CPU core counts.

**RDTSC:** Read Time-Stamp Counter. Malware may use timing differences to detect analysis environments.

**3. Packing and Obfuscation**
- Packing compresses or encrypts the original payload.
- Examples: UPX and custom crypters.
- The payload unpacks itself into memory before execution reaches the OEP.

**OEP = Original Entry Point.**

#### E. Three Real-World Cases

- **Stuxnet (2010):** Targeted industrial infrastructure and Siemens PLCs controlling Iranian nuclear centrifuges. It used four zero-day vulnerabilities and faked normal telemetry.
- **WannaCry (2017):** Ransomware that used EternalBlue against SMBv1 and spread autonomously like a worm.
- **SolarWinds / SUNBURST (2020):** A supply-chain attack involving a backdoor inserted into Orion software updates.

#### F. Important Tools

| Tool | Main Purpose |
|---|---|
| PEStudio | Examine executable files and their properties. |
| CFF Explorer | Inspect PE structures and dependencies. |
| Detect It Easy (DiE) | Inspect file signatures and executable characteristics. |
| FLOSS | Extract and examine strings. |
| YARA | Identify patterns associated with files. |
| IDA Free / Ghidra / Cutter | Examine machine code and assembly. |
| x64dbg / x32dbg / WinDbg | Debug programs, control execution, and inspect memory. |
| ProcMon | Monitor file-system, registry, process, and thread activity. |
| Process Hacker | Inspect process and system activity. |
| Wireshark | Capture and inspect network traffic. |
| Fiddler / PolarProxy | Inspect network communications; the PDF lists these for network interception and C2 traffic analysis. |
| CAPE V2 Sandbox | Observe malware in an isolated analysis environment. |
| ScyllaHide | Help bypass certain anti-debugging checks. |

### 3. Interview Q&A

**Q1. What is malware analysis?**  
Studying malicious software to understand its behaviour, origin, architecture, and capabilities.

**Q2. What are IOCs?**  
Indicators that may help identify a compromise, such as IP addresses, domains, registry keys, and file hashes.

**Q3. Static vs. dynamic analysis?**  
Static analysis examines malware without executing it. Dynamic analysis observes malware running in an isolated environment.

**Q4. What is a worm?**  
Malware that spreads automatically by exploiting network vulnerabilities.

**Q5. What is a rootkit?**  
Malware that can hide processes, files, and network sockets.

**Q6. What is anti-debugging?**  
A technique used by malware to detect or hinder debugging.

**Q7. What is packing?**  
Compressing or encrypting a payload that unpacks itself at runtime.

**Q8. What is the OEP?**  
The Original Entry Point.

**Q9. What is the IAT?**  
The Import Address Table, a PE structure examined during static analysis.

**Q10. What is a sandbox?**  
An isolated environment used to observe suspicious software.

### 4. SOC Analyst Mindset

When malware is suspected, ask:

1. What happened?
2. How did it enter the system?
3. What can it do?
4. How can we detect or stop it?

Remember to:
- Identify relevant IOCs.
- Understand the malware's type and capabilities.
- Examine suspicious processes, files, registry activity, and network connections.
- Choose static or dynamic analysis based on the investigation.
- Recognise when anti-analysis techniques may make investigation difficult.

**Important:** A suspicious indicator is a clue to investigate, not automatic proof of infection.

### 5. Final Memory Map

- **Malware types:** Ransomware, RAT, InfoStealer, Worm, Rootkit, Botnet Client.
- **Analysis:** Static, Dynamic, Code Reversing.
- **Static:** Hashes, strings, PE headers, sections, IAT, YARA.
- **Dynamic:** Processes, files, registry, API calls, network traffic.
- **Evasion:** Anti-Debugging, Anti-VM, RDTSC, Packing.
- **Key terms:** IOC, TTP, C2, PEB, OEP.
- **Cases:** Stuxnet, WannaCry, SolarWinds/SUNBURST.
- **Tools:** PEStudio, Ghidra, x64dbg, ProcMon, Wireshark, YARA.

### Class 35 Recall Checklist

- [ ] Explain the six malware types.
- [ ] Differentiate binary and script malware.
- [ ] Explain static analysis, dynamic analysis, and code reversing.
- [ ] Recall the important IOCs and TTPs.
- [ ] Explain anti-debugging, anti-VM, RDTSC, and packing.
- [ ] Recall the three real-world cases.
- [ ] Match the main tools to their purposes.