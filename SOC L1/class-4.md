# cyber kill chain vs mitre attack
1. Cyber kill chain
cyber kill chain is a model that explains the stages of a cyber attack

stages

| stage | meaning |
|-------|---------|
|reconnaissance|attacker collects target information(domain, employees, network)|
|weaponization|malware / malware or exploit is created to attack the target|
|delivery|the malicious payload is delivered(phishing email, usb, malicious link)|
|exploitation|the attacker exploits a vulnerability to gain access|
|installation|malware is installed on the victim's system|
|command and control|attacker establishes remote control over the compromised system|
|action on objectives|attacker perfroms the final goal(data theft, ransomware, sabotage)|

2. MITRE attack
MITRE ATT&CK is a framework that describes attacker tactics and techniques based on real attacks

main tactics

| tactics | meaning |
|---------|---------|
|reconnaissance|gathering information about the target|
|resource development|preparing infrastructure like domains or servers|
|initial access|gaining entry into the system (phishing, exploit, etc.)|
|execution|running malicious code on the system|
|persistence|maintaining long term access to the system|
|privilege escalation|gaining higher level permissions|
|defense evasion|avoiding detection by security tools|
|credential access|stealing passwords or authentication data|
|discovery|identifying systems, users, and network information|
|lateral movement|moving to other systems inside the network|
|collection|gathering sensitive data|
|command and control| communicating with attacker-controlled servers|
|exfiltration|transferring stolen data outside the network|
|impact|disrupting system (data destruction, ransomware)

# key difference
| cyber kill chain | MITRE ATT&CK |
|------------------|--------------|
|attack stages|attacker techniques|
|high level model|detailed framework|


# TTPs (tactics, techniques, and procedures) in soc

they describe how attackers think, act and operate during a cyber attack.
- if an IOC tells you what happened, TTPs tell you how and why it happened.

soc analysts use ttps to:
- detect attacks even when iocs change
- understand attacker intent
- build better detections, alerts, and response playbook

# why TTPs important in a SOC
imagine this real-world example:
ioc ->> " a masked person was seen"
TTP ->> " the attacker broke the lock, entered through the back door, disabled cctv, and escaped via the fire exit"

soc teams care mote about behavior then just indicators.

# Tactics - The goal
Tactics describe why the attacker is doing something:
common attacker goal:
- gain initial access
- steal credentials
- move laterally
- exfiltrate data
- maintain persistance

# tactics - example
| tactic | meaning |
|--------|---------|
|initial access|how attacker first gets in|
|execution|running malicious code|
|persistence|staying in the system|
|privilege escalation|becoming admin|
|defense evasion|avoiding antivirus/EDR|
|credential access|stealing passwords|
|lateral movement|moving to other system|
|exfiltration|stealing data|

# Techniques - the method 
Techniques describe how the attackers achieves a tactic

Think of techniques as specific attack methods.

For example:

Tactic: credential access

Techniques:
- keylogging
- credential dumping(LSASS)
- browser password theft
- phishing for credentials

each tactic has multiple techniques

# Procedures - the exact steps
Porcedures are the attacker's exact implementation in the real world

This is where:
- tools 
- commands
- scripts 
- timing etc cime into play

example

Technique: credential dumping

procedure command example:
- procdump.exe -accepteula -ma lsass.exe lsass.dmp

most soc teams map ttps using:
MITRE ATT&CK: it is a
- a global knowledge base
- used by SOCs, SIEMs, EDRs, XDRs
- built around tactics and techniques

every soc analyst must know MITRE ATT&CK.


# IOCs = indicatiors of compromise 

they are observable evidence that suggests a system may be compromised or under attack.

If TTPs describe attacker behavior, iocs are the footprints leave behind.

soc analysts hunt, detect, correlate, and respond using locs every single day

ioc = " something bad happended here, and we can prove it with data"

that "data" comes from:
- logs
- network traffic
- endpoint activity
- email headers
- file systems

in a real soc environment, iocs help you:
- trigger alerts in SIEM
- confirm malicious activity
- correlate attacks across sysyems
- respond quickly (block, isolate, contain)
- write incident reports

# types of iocs -1. network based iocs

these show what happened inside the system

example:
- malicious ip address
- suspicious domain
- c2 server communication
- unusual ports or protocols

where soc sees them:
- firewall logs
- proxy logs
- dns logs
- IDS/IPS alerts

2. host/endpoint based iocs
these show what happened inside the system

example:
- suspicious processes
- unexpected services
- registry changes
- new scheduled tasks

where soc sees them:
- EDR/XDR
- windows event logs

3. file based iocs
these related to malicious files

example:
- file hash (MD5, SHA256)
- file name patterns
- file size anomalies

where soc sees them
- antivirus 
- EDR 
- email security gateways
- sandboxes

4. email-based iocs
these relate to malicious emails

example:
- malicious sender email
- phishing subject lines 
- malicious urls
- header anomalies

where soc sees them
- email security tools
- microsoft defender
- proofpoint / mimecast
- user reports

# ioc confidence level
all iocs are not equal at all

| confidence | example |
|------------|---------|
|low |single suspicious ip|
|medium |known phishing domain|
|high |malware hash + execution|
|very high/critical |multiple correlated iocs|

soc analysts never rely on a single ioc

# IOCs vs TTPs

| IOCs | TTPs |
|------|------|
|evidence |behavior |
|what happened |how it happened|
|short-lived |long-lived|
|easy to change |hard to change|
|used for alerts |used for detection logic|

professional socs use both together

# ioc -> alert -> investigation (real soc flow)

1. ioc detected (ip / hash / process)
2. SIEM generates alert
3. soc l1 validated ioc
4. soc maps to ttp
5. decision: true positive or false positive
6. escalation or closure

# alert triage
alert triage is the process of quickly analyzing security alerts to determine whether they are:
- real threat
- false positive
- needs escalation

simple meaning
alert triage = separating real attacks from normal noise quickly

# why alert triage is important
soc environments generate thousands of alerts daily, but only a small percentage are real incidents

soc analyst responsibilites:
- filter alerts
- prioritize alerts
- investigate suspicious activity

# how alerts are generated
1. event occurs (login, process execution, file download)

2. system logs the event (os / firewall / cloud)

3. logs are sent to SIEM / EDR

4. security tool generated alerts for suspicious activity

key point

alerts help soc analyst focus on suspicious events instead of millions of raw logs

# alert tirage workflow

Alert sources

Security alerts can come from:
- SIEM
- EDR / XDR
- IDS / IPS
- email security tools
 
Triage analyst role

soc l1 analyst:
- monitors alerts
- investigates suspicious activity
- filters false positives
- escalates real threats

Investigation data sources

to analyze alerts, soc analysts use:
- system logs 
- endpoint logs
- cloud logs
- network logs

playbooks
soc teams use playbooks (soar) to:
- automate investigation steps 
- standardize incident response

final actions

after investigation
- false positive -> close alert
- real incident -> escalate to l2/l3

Real soc flow
```
security tool -> alert -> soc triage -> investigation -> decision -> escalation/closure
```
# why alert triage is critical

without proper triage:
- soc teams drown in alerts 
- real attacks get missed
- response is delayed
- business impact increases

with good triage:
- false positive are reduced
- real threats are caught early
- soc becomes efficient and trusted

soc analyst are promoted based on triage quality, not number of alerts closed

triage decides whether an alert becomes an incident

# alert properties

| property | meaning (soc l1) | example |
|----------|------------------|---------|
|alert time |when the alert was generated |mar 21, 15:35|
|alert name |summary of what triggered |unusual login location|
|alert severity |urgency assigned by detection |low/medium/high/critical|
|alert status |current lifecycle state |new / in progress / closed|
|alert verdict |l1 classification outcome |true positive / false positive|
|alert assignee |analyst handling the alert |assigned analyst name|
|alert description |explanation of what the alert means |detailed description of the suspicious activity|
|alert field |contextual values that led to the alert |affected hostname, entered commandline, etc|

# alert prioritisation
alert prioritisation is the process of deciding which alert should be investigated first

soc teams define prii=oritisation rules in SIEM or EDR

1. filter alerts
- ignore alerts already investigated by other analysts
- focus only on new and unresolved alerts

2. sort by severity
investigate alerts in this order:
```
critical -> high -> medium -> low
```

critical alerts usually indicate serious threats

3. sort by time
start with older alerts first, then move to newer ones.

reason: older alerts may indicate attackers already progressing in the attack

# soc alert investigation flow
```
discovery
|
preliminary investigation
|
triage
|
extended investigation
|
containment / response
```

# alert triaging
alert triaging is the process of quickly analyzing alerts to determine if they are real threats or false positives

# initial actions (soc l1)
before investigation:
1. assign the alert to yourself
2. change alert status to in progess
3. review alert details:
- alert name
- description
- severity
- indicators(ip, domain, process)

this ensures ownership of the alert and avoids conflict with other analysts

# investigation steps
during investigation soc analysts should:

1. identify the affected entity
- user
- hostname
- network
- cloud system
- website

2. understand the activity
example:
- suspicious login
- malware activity
- phishing email

3. review surrounding events
look at logs before and after the alert to find suspicious activity

4. use threat intelligence
use threat intelligence platform to verify indicators such as:
- ip addresses
- domains
- hashes

