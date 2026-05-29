# class 5 | Alert reporting, escalation and cyber kill chain

# Cyber kill chain methodology
- cyber kill chain - attacker lifecycle
- hacking methodologies- practical execution flow

the cyber kill chain is a framework created by lockheed martin to explain how cyber attacks happen step by step

it is a linear model that focuses on the attackers journey from the outside in. by breaking the chain at any point, you stop the entire attack

# the cyber kill chain
stages of a cyber attack

1. reconnaissance - gathering information on target

examples
- researching company and employees
- finding emails and usernames
- identifying target systems and vulnerabilities

2. Weaponization - crafting the malicious payload

examples
- creating malicious attachments or  links
- developing malware or exploits

3. Delivery - sending the weapong to target

examples
- phishing emails with malicious links or atachments
- malicious website or drive-by downloads

4. exploitation - exploiting the vulnerability

examples 
- run malware or exploit code
- trick user into enabling macros
- infected usb drives

5. installation - installing malware on system

examples
- install malware/backdoors
- create persistence in the system
- exploit unpatched software vulnerabilities

6. command and control - remote conrol of compromised system

examples
- communicate with attacker c2 server
- execute commands remotely

7. action on objectives - deploy ransomware or launch ddos

examples 
- steal data and sensitive information
- move laterally through network
- deploy ransomware or lauch ddos

# 7 stages of cyber kill chain
|phase |description |key ethical hacking activity |
|------|------------|-----------------------------|
|reconnaissance |gathering intel on the target(osint) |passive and active footprinting |
|weaponization |coupling an exploit with a backdoor(eg. a pdf with a script) |payload crafting with metasploit/cobalt strike |
|delivery |sending the weapon to the victim (email, usb, web) |phishing simulations |
|exploitation |the "boom" moment - triggering the vulnerability |executing a buffer overflow or sql injection |
|installation |installing persistent malware on the victims asset |setting up persisten shells or rootkits |
|c2(command) |establishing a remote channel for control |configuring c2 frameworks like mythic or havoc |
|actions |final goals: data theft, encryption, or destruction |data exfiltration testing (dlp bypass) |

# Reconnaissance (information gathering)

what happens here?
- attacker collects information about the target without touching it directly(mostly)

attackers mindset:
- before attacking, i must know who, what, where, and how.

real-world examples:
- findings employee emails
- identifying company domains and subdomains
- findings technologies used(wordpress, apche,IIS)
- studying linkedin profiles
- findings leaked passwords

tools and techniques:
- google dorking
- whois lookup
- dns enumeration
- osint (open source intelligence)

defensive view(soc):
- monitor excessive dns queries
- track scanning behavior 
- watch unusual osint-based phishing patterns

# Weaponization
what happens here?
- attacker prepares a payload + exploit
payload = what runs after exploit
exploit = how vulnerability is abused

example:
- malware embedded in a pdf
- reverse shell hidden in word macro
- exploit for an unpatched service

attackers mindset:
- i have info. now i build the weapon

soc perspective:
- file hash analysis
- malware sandboxing
- detect known exploit signatures

# delivery
what happens here?
- weapon is delivered to the victim

common delivery methods:
- phishing email
- malicious attachment 
- drive by website
- usb drop
- compromised ads

example:
- hr receives a "resume.pdf.exe" via email

soc controls:
- email gateway filtering
- url reputation
- attachment sandboxing

# exploitation
what happens here?
- the vulnerability is actually triggered

example:
- user clicks malicious link
- software buffer overflow
- outdated plugin exploited
- macro execution

Important concept:
- no exploitation = no compromise

soc teams try to break the chain here

# installation
what happens here?
- malware installs persistence

persistence means?
- even if system restarts, i stay.

techniques:
- registry run keys
- scheduled tasks
- startup folders
- backdoor users

soc focus:
- endpoint detection and response(EDR)
- registry monitoring
- autorun analysis

# command and control(c2)
lifecycle of a command and control
```
1. initial compromise 
- phishing email/exploit
|
2.malware installed 
- malware deployed on host
|
3. c2 channel established
- c2 connection(phone home)
|
4. commands issued
- remote control by attacker
|
5. data exfiltrated / lateral movement
- exfiltration or internal spread
```

what happens here?
compromised system talks to attackers server

examples:
- beconing every 60 seconds
- dns tunneling
- https based c2

soc detection:
- abnormal outbound traffic
- beaconing patterns
- known bad ips/domains

# action on objectives
what happens here?
- attacker does what they came for

objectives include:
- data theft
- ransomware deployment
- credential dumping
- lateral movement
- financial fraud

this is where maximum damage happens

# standard hacking methodologies
reconnaissance: 
- collecting information (ips, dns, employee names)

scanning:
- using tools like nmap or nessus to find open ports and live services

gaining access:
- this is the actual "hack" - breaking through the perimeter or using credentials

mainataining access:
- ensuring you dont lose your connection if the user reboots or the network resets(persistence)

clearing tracks:
- deleting logs and removing tools to avoid detection by the blue team(defenders)

# Cyber Kill Chain vs Hacking Methodology
|Cyber Kill Chain |hacking methodology |
|-----------------|--------------------|
|Reconnaissance |reconnaissance |
|Weaponization |exploit prep |
|Delivery |payload delivery |
|Exploitation |gaining access |
|Installation |maintaining access |
|C2 |persistent control |
|Actions |post exploitation |

# alert reporting (documentation) -1
what is alert reporting?
aler reporting is the process of formally documenting:
- what was detected
- what was analyzed
- what conclusion was reached
- what action was taken or recommended

if its not documented, it didn't happen (soc golden rule)

# alert reporting (documentation) - 2
why alert reporting matters
- create audit trail
- enables handover between shifts
- supports incident response
- protects analysts legally
- helps improve detections

in real socs, bad reporting = bad analyst, even if triage was correct

# alert reporting (documentation) - 3
example: Tier-1 alert report (short)
summary: 
- powershell executed with encoded command triggered word document on finance user system

analysis:
- execution occurred outside business hours. parent process was winword.exe. external conncetion observed

verdict:
- true positive - suspicious execution

recommendation:
- escalate to soc l2 for containment

that's it clear, facutal,defensible

# alert escalation - 1
what is escalaton?
escalation means:
- this alert is beyond tire-1 authority and requires higher expertise or action

tier-1 does not fix incidents
tier-1 identifies and hands over correctly

# alert escalation-2
when should tier-1 escalate?
escalate when any of the following are true:
|condition | example |
|----------|---------|
|confirmed malicious activity |malware execution |
|privileged account invloved |admin user |
|critical asset affected |server / dc |
|multiple alerts correlated |phishing + execution |
|data risk exists |possible exfiltration |
|policy requires escalation |severity high/critical |

escalation is not failure, its professionalism

# alert escalation-3
example: tier-1 escalation note

escalation reason:
- confirmed suspicious powershell execution with external communication

evidence attached:
- process tree, command line, destination domain

severity:
- high

recommended action:
- endpoint isolation and memory analysis

this makes l2 trust you instantly

# soc communication (the most underrated skill) -1 
what is soc communication?
soc communication is:
- analyst -> analyst
- analyst -> ir team
- analyst -> IT/admin
- soc -> management

your are translating techincal riskinto actionable information

# soc communication(the most underrated skill) - 2
communication principle (soc standard)
- clear
- factual
- no assumptions
- no panic language
- no blame 

wrong = system hacked badly!!!
right = suspicious activity detected, under investigation

# communication types in soc

internal soc communication
used during:
- shift handover
- escalation
- collaboration

example(handover note):
- alert escalated to l2. endpoint pending isolation. monitoring ongoing

# IT/admin communication
used when action is needed

example:
- please isolate FIN-LAP-07 from the network as suspicious activity was detected

not:
- there is malware everywhere

# Management communication(high level)

management doesn't want logs
they want impack + status

example:
- suspicious activity detected on one fincance user system. no evidence of data exfiltration so far. incident under investigation

# How reporting, escalation and communication fit together
How Reporting, Escalation & Communication Fit Together
Alert Detected
     ↓
Alert Triage
     ↓
Alert Report Written
     ↓
Escalation (if needed)
     ↓
Clear Communication
     ↓
Action Take