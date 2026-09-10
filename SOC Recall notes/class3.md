# Day 3 (Part 2) – Major System Categories & Misconfigurations

# 🚀 30-Second Recall
- Misconfiguration ≠ Vulnerability.

- Misconfiguration = Wrong/Securely poor setup.

- Most breaches occur due to misconfigurations & unpatched systems.

- Cloud Misconfigurations = Public S3, Open Blob Storage, Exposed Keys.

- Network Misconfigurations = Open Firewall, No Segmentation.

- Identity Misconfigurations = No MFA, Shared Admin, Excessive Privileges.

- Endpoint Misconfigurations = Antivirus Off, Local Admin, USB Enabled.

- Endpoints = Laptops, Desktops, VDI, Workstations.

- Users are the weakest security point.

- Endpoint attacks = Phishing, USB Malware, Drive-by Downloads.

- Servers = Web, App, Database, File.

- Server attacks = Log4j, SQLi, RCE, Weak Credentials.

- Network Devices = Routers, Firewalls, VPNs, Load Balancers.

- Device attacks = Firmware Exploits, Default Passwords, VPN Bugs.

- Cloud Systems = AWS, Azure, GCP.

- Cloud attack vectors = Public Buckets, IAM Abuse, Metadata Abuse.

- sOC monitors logs to detect misconfigurations before attackers exploit them.

# 📌 Must Remember
Misconfiguration
- A misconfiguration is not a software bug.

It is a mistake made while configuring a system.

Examples:
- Default Passwords
- Public Storage
- Excessive Permissions
- Firewall Misconfiguration

Cloud Misconfigurations

Examples
- Public S3 Bucket
- Open Azure Blob Storage
- Exposed Access Keys
- Over-Permissive IAM Roles

SOC Example
```
Public S3 Bucket

↓

Sensitive Data Indexed

↓

Data Breach
```
Network Misconfigurations

Examples
- Firewall Allows All Traffic
- Internal Services Exposed
- No Network Segmentation

SOC Example
```
Database Port Open

↓

Internet Scan

↓

Database Accessed
```
Identity Misconfigurations

Examples
- MFA Disabled
- Shared Admin Accounts
- Excessive Group Membership
- Over-Privileged Users

SOC Example
```
Compromised User

↓

Already Administrator

↓

No Privilege Escalation Needed
```
Endpoint Misconfigurations

Examples
- Antivirus Disabled
- No EDR
- Local Administrator
- USB Allowed

SOC Example
```
Malware Executes

↓

No Protection

↓

Persistence Achieved
```
# Major System Categories
Endpoints

Examples
- Laptop
- Desktop
- VDI
- Workstation

Attack Methods
- Phishing
- USB Malware
- Drive-by Download
- Unpatched Software

Why Dangerous?
- Users Click Links
- Users Execute Files
- Weakest Security Point

# Servers
Types
- Web Server
- Application Server
- Database Server
- File Server

Common Attacks
- Log4j
- SQL Injection
- RCE
- Weak Credentials
- Exposed Services

Why Valuable?
- Store Sensitive Data
- Run Business Applications
- Trusted Internally
- Network Devices

Devices
- Router
- Firewall
- VPN Gateway
- Load Balancer

Attack Methods
- Default Credentials
- VPN Vulnerabilities
- Firmware Exploits
- Firewall Misconfiguration

# Cloud Systems

Platforms
- AWS
- Azure
- GCP

Common Attack Vectors
- Public S3 Bucket
- Exposed Access Keys
- Over-Permissive IAM
- Metadata Service Abuse

# SOC Detection Focus
SOC Analysts should monitor:
- Firewall Logs
- IAM Logs
- Endpoint Logs
- VPN Logs
- Cloud Logs
- Authentication Logs
- SIEM Alerts
- EDR Alerts

# 💼 Interview Q&A
1. What is a Misconfiguration?

A security weakness caused by incorrect system configuration rather than a software bug.

2. Why are Misconfigurations dangerous?

Because attackers exploit them without needing advanced exploits.

3. Name common Cloud Misconfigurations.
- Public S3 Bucket
- Open Blob Storage
- Exposed Keys
- Over-Permissive IAM

4. Name common Network Misconfigurations.
- Open Firewall
- No Network Segmentation
- Exposed Internal Services

5. Name common Identity Misconfigurations.
- No MFA
- Shared Admin Accounts
- Excessive Permissions

6. Name common Endpoint Misconfigurations.
- Antivirus Disabled
- No EDR
- Local Admin Rights
- USB Enabled

7. What are Endpoints?

User devices such as laptops, desktops, VDIs and workstations.

8. Why are Endpoints the most targeted?

Because users interact with emails, links, USB devices and downloaded files.

9. Name common Endpoint attacks.
- Phishing
- USB Malware
- Drive-by Downloads
- Exploiting Unpatched Software

10. Name different Server types.
- Web Server
- Application Server
- Database Server
- File Server

11. Why are Servers high-value targets?

Because they host business applications and sensitive organizational data.

12. Name common attacks against Servers.
- Log4j
- SQL Injection
- Remote Code Execution
- Weak Credentials
- Exposed Services

13. Name common Network Devices.
- Router
- Firewall
- VPN Gateway
- Load Balancer

14. Name common Cloud attack vectors.
- Public Buckets
- IAM Abuse
- Exposed Access Keys
- Metadata Service Abuse

15. What logs should a SOC analyst check for Misconfiguration alerts?

Firewall Logs, IAM Logs, VPN Logs, Endpoint Logs, Cloud Logs, SIEM Alerts and EDR Alerts.

# 🛡️ SOC Analyst Mindset

Whenever a misconfiguration alert is generated, think in this order:
```
Step 1 – What is misconfigured?
 Cloud Resource?
Firewall?
User Account?
Endpoint?
Server?
Network Device?

↓

Step 2 – Can an attacker exploit it?

Examples:

Public Storage?
Default Password?
No MFA?
Open Port?
Admin Rights?
Disabled Antivirus?

↓

Step 3 – Check Logs
SIEM
EDR
Firewall
VPN
IAM
Cloud Logs
Authentication Logs

↓

Step 4 – Determine Impact
Data Exposure?
Unauthorized Access?
Privilege Escalation?
Lateral Movement?
Malware Execution?

↓

Step 5 – Mitigate
Close Public Access
Enable MFA
Patch System
Restrict Permissions
Disable Compromised Account
Escalate if Required
```
SOC Investigation Checklist
- ✔ Which asset is affected?

- ✔ What type of misconfiguration exists?

- ✔ Is anyone exploiting it?

- ✔ Which logs confirm the activity?

- ✔ What is the business impact?

- ✔ How can the risk be removed?

L1 SOC Rule
- Misconfiguration → Exploitation → Incident
- Find the weakness before an attacker does.

# 📝 Question Paper Mode
1. What is a Misconfiguration?

2. How is a Misconfiguration different from a Vulnerability?

3. Name common Cloud Misconfigurations.

4. Name common Network Misconfigurations.

5. Name common Identity Misconfigurations.

6. Name common Endpoint Misconfigurations.

7. Why are Public S3 Buckets dangerous?

8. Why is disabling MFA considered a security risk?

9. Why are Endpoints the most targeted systems?

10. Name common Endpoint attack methods.

11. Name different Server types.

12. Why are Servers valuable targets?

13. Name common attacks against Servers.

14. Name common Network Devices.

15. Name common attacks against Network Devices.

16. Name major Cloud platforms.

17. Name common Cloud attack vectors.

18. What logs should be checked during a Misconfiguration investigation?

19. What should a SOC analyst investigate after detecting a Public S3 Bucket?

20. What should a SOC analyst investigate after detecting disabled Antivirus on an endpoint?

21. Explain the SOC investigation workflow for Misconfiguration alerts.

22. Why are excessive IAM permissions dangerous?

23. Why are default credentials dangerous?

24. Explain the difference between Endpoint, Server, Network Device and Cloud System.

25. Explain the attack chain from Misconfiguration to Incident.

# ✅ Answer Key

1. A security weakness caused by incorrect configuration of a system, not by a software bug.

2. 
- Misconfiguration: Incorrect or insecure setup.
- Vulnerability: A flaw or weakness in software, hardware or a process.

3. 
- Public S3 Buckets
- Open Azure Blob Storage
- Exposed Access Keys
- Over-Permissive IAM Roles

4. 
- Open Firewall Rules
- No Network Segmentation
- Exposed Internal Services

5. 
- No MFA
- Shared Admin Accounts
- Excessive Permissions
- Over-Privileged Users

6. 
- Antivirus Disabled
- No EDR
- Local Administrator Rights
- USB Access Enabled

7. Because anyone with access may view or download sensitive data, leading to data exposure or breaches.

8. Without MFA, stolen credentials alone can allow attackers to access accounts.

9. End users frequently interact with emails, websites, USB devices and downloaded files, making endpoints the easiest entry point.

10. 
- Phishing
- USB Malware
- Drive-by Downloads
- Exploiting Unpatched Software

11. 
- Web Server
- Application Server
- Database Server
- File Server

12. Servers host critical applications and sensitive organizational data, making them high-value targets.

13. 
- Log4Shell (Log4j)
- SQL Injection
- Remote Code Execution (RCE)
- Weak Credentials
- Exploitation of Exposed Services

14. 
- Router
- Firewall
- VPN Gateway
- Load Balancer

15. 
- Default Credentials
- Firmware Exploits
- VPN Vulnerabilities
- Firewall Misconfiguration

16. 
- AWS
- Microsoft Azure
- Google Cloud Platform (GCP)

17. 
- Public Storage Buckets
- Exposed Access Keys
- IAM Abuse
- Metadata Service Abuse

18. 
- SIEM Logs
- EDR Logs
- Firewall Logs
- VPN Logs
- IAM Logs
- Cloud Logs
- Authentication Logs

19. 
- Whether sensitive data is exposed
- Who accessed the bucket
- Access logs
- Bucket permissions
- Immediate remediation (remove public access)

20. 
- Why antivirus is disabled
- Recent malware alerts
- Suspicious processes
- User activity
- EDR status
- Signs of compromise

21. 
- Alert → Identify Misconfiguration → Analyze Logs → Assess Impact → Mitigate → Escalate (if required).

22. Excessive IAM permissions allow attackers to perform unauthorized actions or escalate privileges after compromising an account.

23. Default credentials are publicly known or easily guessed, making unauthorized access much easier.

24.
- Endpoint: User device (laptop, desktop, workstation)
- Server: Hosts applications and data
- Network Device: Controls and routes network traffic
- Cloud System: Resources hosted on cloud platforms like AWS, Azure or GCP

25. Misconfiguration → Attacker Discovers Weakness → Exploitation → Unauthorized Access → Data Theft/Privilege Escalation → Security Incident