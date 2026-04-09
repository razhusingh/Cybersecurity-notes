# The 3 soc operating models

1. in-house(internal)soc
a company builds and runs its own soc internally using its own people, tools and processes.

2. outsourced / managed soc (MSP/MSSP SOC)
a third party security company (MSSP) provides soc services to multiple client organizations

MSP: managed service providers
MSSP: managed security service providers

3. hybrid soc (co-managed soc)
a shared responsibility model between:
- internal soc team and external MSSP

# system as attack vectors
a system becomes an attack vector when an attacker uses it to:
- gain initial access
- move laterally
- maintain persistence
- exfiltrate data
- launch further attacks

# human oriented attacks
users are those who start the attack mostly: (before external factors, users are responsible at first)

example:
- rubber ducky
- keyloggers binded with legitimate softwares
- clicking on suspicious links
- opening any email or sent attachments
- storing passwords at unsecure portals
- trusting soon
- using outdated/pirated softwares etc

# supply chain attacks
if threat actors manage to breach one of the apps or libraries and push an update to all its users, all of them will be compromised, this technique is called supply chain attacks

# vulnerabilities
A vulnerability is a flaw or weakness in a system that can be exploited to compromise confidentiality, integrity, or availability

example:
- software bugs
- misconfiguration
- weak passwords
- outdated systems

# software vulnerabilities
example of software vulnerabilites:
- sql injection
- command injection
- buffer overflow
- cross site scripting (xss)
- remote code execution(RCEL)

SOC detection:
- WAF alerts
- web server logs
- unusual post request
- EDR alerts on servers

# operating system vulnerabilities
example of operating system vulnerabilites
- windows vulnerabilites
- linux vulnerabilities
- mac os kernels or service vulnerabilities etc

for example: privilege escalation bugs, SMB vulnerabilities (eternallbue), kernal exploits etc

soc detection:
- sudden privilege changes
- exploit behavior in EDR
- kernel driver loading alerts etc.

# network vulnerabilities
example of network vulnerabilites:
- open ports
- weak protocols (telnet, FTP)
- unpatched routers/firewalls
- exposed admin interfaces

soc detection
- IDS/IPS alerts
- firewall logs
- excessive authentication failures

# authentication and authorization vulnerabilities
example of authentication and authorization vulnerabilites:
- weak passwords
- no MFA 
- broken access control
- privilege ascalation paths

soc detection:
- IAM alerts
- access logs
- role change events

# configuration dependent vulnerabilites
example of configuration dependent vulnerabilities:
- debug mode enabled
- default credentials
- excessive permissions

soc detection
- admin panel exposed
- default credentials unchanged 
- system takeover

# zero-day vulnerabilities
a zero day vulnerability is a security flaw in software or a system that is unknown to the vendor and for which no patch or fix is available yet. attackers can exploit it before it is discovered or patched.

soc detection:
- abnormal processes
- suspicious network traffic
- lateral movement

vulnerability: weakness exists
exploit: vulnerability is abused
incident: damage or compromise occurs

# life cycle of a zero day
1. vulnerability discovery
a new security flaw or weakness is discovered in software or a system

2. exploit development
attackers discover or create a method to exploit the vulnerability

3. exploitation/attack
cybercriminals exploit the vulnerability to gain access, steal data, or cause damage

4. vendor discovery
the software vendor becomes aware of the vulnerability

5. patch release
the vendor releases a patch or update to fix the vulnerability

```
discover-> exploit-> attack -> detect -> patch

```
why is zero day dangerous?
because the vulnerability is unknown to the vendor and no patch is available, attackers can exploit it before it is fixed

# common misconfigurations for soc:
misconfiguration isn't a bug in the software but a mistake in how the system was set up, often by the IT TEAM. These errors happen frequently, usually to make things simpler like using "1111" instead of typing a long password everytime

# cloud msiconfiguration
- public s3 buckets
- open azure blob storage
- over-permissive IAM roles
- exposed access keys

soc example:
```
s3 bucket public
|
sensitive data indexed by search engines
|
data breach
```

# network misconfigurations
- firewall allows all traffic
- internal services exposed externally
- no network segmentation (all devices on same network)

soc examples:
```
internal DB port exposed
|
external scan finds it
|
database accessed

```
# identity misconfigurations
- MFA disabled for admins
- excessive group membership
- shared admin accounts

soc example:
```
compromised user
|
user already has admin privileges
|
no escalation needed

```

# endpoint misconfigurations
- antivirus disabled
- local admin access
- usb allowed everywhere

soc example:
```
malware executed
|
no EDR
|
persistence established

```
" most breaches don't happen because of zero-day they happen because of misconfiguration and unpatched vulnerabilities"


# major system categories used as attack vetcors
Endpoints:
what are endpoints?
- laptops
- desktops
- VDI ( virtual desktop infrastructure)
- workstations

how attackers use them:
- phishing emails -> malicious attachments
- drive by downloads
- usb based malware
- exploiting unpatched software

why endpoints are dangerous:
- users have access
- users click things
- often weakest security point

Servers(application / database / file)
types:
- web server
- app server
- DB server
- file server

how attackers abuse servers:
- exploiting
- log4j
- sql injection
- RCE vulnerabilities
- weak admin credentials
- exposed services

why servers are high value:
- run critical apps
- store sensitive data
- often trusted internally

Network devices (routers, firewalls, vpns)
devices:
- routers
- firewalls
- vpn gateways
- load balancers

how attackers abuse them:
- default credentials
- vpn vulnerabilities
- misconfigured firewall rules
- firmware exploits

# cloud systems (aws / azure / gcp)
common cloud attack vectors:
- public s3 buckets
- exposed access keys
- over-permissive IAM roles
- metadata service abuse
