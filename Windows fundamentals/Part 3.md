# Windows fundamentals part 2

# windows updates
purpose:
- keeps system secure and updated
- fixes vulnerabilities and bugs

types of updates:
- security updates -> fixes security issues
- feature updates -> new features
- quality updates -> performance improvements

important:
- updates protect system from new threats

# windows security
windows security is built in protection in windows

main components:
- virus and threat protection
- firewall and network protection
- account protection
- device security
- app and browser control

purpose:
- protect system from malware and attacks

# virus and threat protection
managed by microsoft defender antivirus.

function:
- detect malware
- scan files and programs
- remove threats
- real time protection

types of scans:
- quick scan
- full scan
- custom scan

# firewall and network protection
firewall = network security system
firewall monitors incoming and outgoing network traffic

purpose:
- protect system from network attacks
- blocks unauthorized access

example: like a security guard at the gate of a building

types of firewall profiles:
- domain network
- private network
- public network

# app and browser control
protects system from malicious applications and websites

features:
- microsoft defender smartscreen
- reputation based protection
- exploit protection

purpose:
blocks dangerous apps and downloads

# device security
protects hardware and sytem integrity

key features:
- core isolation
- secure boot
- TPM (Trusted platform module)

purpose: prevent low level malware attacks

# bitlocker
disk encryption tool

purpose:
- protect data if device is lost or stolen
- encrypts entire disk

important point: without the bitlocker key data cannot be accessed

# volume shadow copy service (vss)
vss creates backup snapshots of files

purpose:
- allows file recovery
- restore previous versions of files

example: if ransomware deletes files -> previous copies may be recovered

soc analysts sometimes check this during incident response

# windows security tools
important built-in tools:

task manager

shows:
- running applications
- cpu usage
- memory usage
- processes

event viewer

used to:
- view system logs
- analyze errors
- investigate security events

soc analysts often check logs here.

# windows defender firewall
controls:
- network traffic
- application access
