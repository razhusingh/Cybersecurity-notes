# As a Tier-1 SOC Analyst, you are the first responder. you monitor, triage, escalate, and document every security alert.
- Monitor SIEM, EDR/XDR, firewall, email alerts
- Validate alerts: True positive or False positive
- Escalate critical events to Tier-2/IR
- Log everthing in ticketing systems

# Core concept
The main focus of the SOC team is to keep Detection and Response intact

# Soc team structure
CISO
|
SOC Manager
|
SOC analyst l1, SOC L2, SOC L3, Security Engineer, Detection Engineer

# People
SOC Analyst(l1):
- perform initial triage 
- monitor alerts
- Escalate suspicious activity

SOC Analyst(l2):
- Investigate alerts
- Analyze logs
- perform deeper threat analysis

SOC Analyst(l3):
- Advanced investigation
- Threat hunting
- Malware analysis

Security Engineer:
- Manage security tools
- Configure SIEM / EDR
- Maintain SOC infrastructure

Detection Engineer:
- Create detection rules
- Improve alert accuracy
- Reduce false positives

SOC Manager:
- Leads the SOC team
- Reports security incidents to CISO (Chief information security officer)
- Ensure SOC tools and processes work properly

# Process
Alert triage:
The alert triage is the basis of the soc team. the first response to any alert is to perform the triage

Alert triage = investigating an alert using the 5 W's
- what? -> type of incident
- when? -> time of incident
- where? -> affected system
- who? -> affected user
- why? -> root cause

Reporting
- harmful alerts should escalated to higher level analyst

report should include:
- incident details
- analysis summary
- screenshots / evidence
- explanation using the 5 Ws

Incident response and forensics
high level teams handle critical incidents

- contain the threat
- investigate root cause
- perform forensic analysis

# Technology
The technology portion in the soc pillars refers to the security solutions.

# Some of these security solution:
SIEM:
- central platform for security monitoring
- collects logs from various network devices.
- detection rules are configured in the SIEM solution
- provides user behavior analystics and threat intelligence capability

note: the SIEM solution only provides the detection capabilities in a soc environment

EDR(Endpoint detection and response):
- provides detailed real time and historical visibility of the devices activities
- detects suspicious behavior on endpoints
- supports automated responses
- helps investigate and respond to threats

Firewall
- acts as a barrier between internal and external networks
- monitors incoming and outgoing traffic
- blocks unauthorized or suspicious traffic
- uses detection rules to protect the network

Other security tools in soc

antivirus / EPP -> protects endpoints from malware

IDS / IPS -> detects and prevents network attacks

XDR -> extended detection across multiple systems

SOAR -> automates security operations and response

short meaning
SIEM -> log monitoring and detection
EDR -> endpoint detection and response
FIREWALL -> network traffic filtering
IDS/IPS -> intrusion detection and prevention
SOAR -> automation of security operations

# Security departements

RED TEAM: offensive security experts, pentesters or ethical hackers who look for security issues

GRC TEAM : specialists managing policies and ensuring compliance with regulations like PCI DSS

BLUE TEAM: defensive security experts like soc analysts, engineers, or incident responders

L1: junior members who triage alerts and pass comples cases to l2
L2 analysts: experienced members who investigate more advanced attacks
Engineers: Experts in configuring security tool like EDR or SIEM
Manager: A person who manages the whole SOC Team

# Human vector in soc
why humans are targeted?
- humans are targeted because of the access they can provide to website, mailboxes, or databases.

how humans are targeted
- phishing attacks
- malware downloads
- deep fakes
- impersonation
- other attacks like keylogging, physical attacks etc

how to defend humans
- anti phishing solutions : detect and block phishing emails
- antivirus / EDR : detect malware on endpoints
- " trust but verify " principle : verify users and actions before trusting
- security awareness training : educate employees about phishing and social engineering
