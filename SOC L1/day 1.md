# SOC (security operation center)
purpose
> minimize dwell time(time attacker stays hidden)
> first line of defence 
> 24*7 monitoring to detect, analyze and respond to threats

# Difference between soc vs noc vs IR team
SOC -
monitor security events
detect threats
analyzes alerts

NOC -
monitor network performance, uptime, bandwidth issues

IR team -
respond to the confirmed incident, perform forensics, containment and recovery

also think it like:-
- soc as watchtower constantly scanning for enimies
- noc as maintaining castle walls
- IR team are special force deployed when attack breach defences

# duties as a soc analyst
> monitor and invistigate security threats
> participate in security workshop
> collaborate with security teams
> constantly learn new attacks and defenses

# soc analyst l1: role on the front line
1) monitor and triage alerts 
watch SIEM dashboard
perform initial triage 
check logs

2) analyze and document
analyze logs(windows event, firewall, proxy)
document investigation findings

3) Escalate or close
close alert if false positve
escalate to l2/l3 for deeper investigation

# attack scenarios: defender's perspective

> phishing attack
indicators:
email gateway alerts
user clicking suspicious link
outbound connection to new domain

action -> check email headers, verify domain reputation, isolate user endpoint if compromise suspected

> malware execution
indicators:
EDR alert on suspicious process
unsigned executable
outbound beacon to c2 server

action -> quarantine file, check hash in virustotal, document IOCs, escalate for forensics

> ransomware
mass file encryption
ransom note creation
unusual disk activity
backup deletion attempts

action: immeditate escalation, isolate affected systems, document timeline, notify IR team

> brute force
multiple failed logins attempts (event id 4625)
account lockouts
login from unusual locations

action: verify legitimate user activity, block source ip, check compromise, reset credentials

# alert triage: your decision making framework
1) initial assessment
read alert description
check severity rating 
note affected asset

quick context: is this a critical server or user workstation? business hour or 3 AM

2) log analysis
query SIEM logs
check 30 min before/after alert
analyze ip, user, process, frequency

3) context gathering
is source ip internal or external?
is user account legitimate? 
check threat intelligence sources
verify if IP/domain is malicious
any similar alerts recently?

4) decision
true positive? escalate with documentation
false positive? close with clear justification
unsure? escalate- better safe than compromised


true positive indicatiors
> connection to known malicious ip/domain
> unusual time of activity (3am access to finance data)
> privilege escalation attempts
> data exfiltration patterns (large uploads to cloud storage)
> multiple failed logins followed by success

common false positive
> automated system scans triggering port scan alerts
> legitimate admin activity flagged as suspicious
> poorly tuned SIEM rules with low thresholds
> benign software triggering EDR heuristics
> scheduled tasks appearing as unusual processes