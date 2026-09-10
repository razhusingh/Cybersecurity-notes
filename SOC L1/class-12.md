# Class 12 - MITM and DDOS

# MITM (Man in the middle attack)
Goal of MITM
- Steal credentials
- capture session cookies
- modify data in transit
- inject malware
- monitor sensitive communication

# Types of MITM attacks
1. ARP spoofing (very important for soc)
- Attacker tricks devices into thinking:

" i am the router "

so traffic goes through attacker

example flow:
- victim -> attacker -> router -> internet

soc indicators
- duplicate MAC addresses
- ARP table changes
- sudden traffic rerouting
- internal network anomalies

2. Dns spoofing 
- Attacker redirects domain to fake ip.

example
- google.com -> attacker server

very similar to pharming

3. SSL stripping
- attacker downgrades: HTTPs -> http

user thinks connection is secure but it's not

4. Session hijacking
- attacker steals session cookies and logs in without password

example:
- user logs into website
- attacker steals cookie
- attacker gains access

5. Evil twin
Fake wifi network:
- user connects
- attacker intercepts all traffic

# Real soc scenario (MITM)
Alert:
- multiple users accessing same gateway ip
- ssl certificate mismatch
- suspicoious dns responses

Investigation:
- check ARP table
- check Dns logs
- check network traffic anomalies

# MITM prevention
- https (tls encryption)
- vpn usage 
- secure dns (DNSSEC)
- Certificate validation
- network segmentation
- WPA3 wifi security

# DDOS (distributed denial of service)
what is DDOS?
A ddos attack flood a system with massive traffic to make it:
- slow 
- unresponsive 
- completely down

# Goal of DDoS:
- take website offline
- disrupt business operations
- extortion ("pay or we keep attacking")
- diversion for other attacks

# Real soc example
- alert:

Traffic increased from 2k req/sec -> 200k req/sec

source: multiple countries

endpoint: /login

likely: application layer ddos

# Types of DDoS attacks
1. Volumetric attacks
Flood network bandwidth

example:
- UDP lood
- ICMP flood

2. protocol attacks
target server resources

example:
- SYN flood
- ping of death

3. Application layer attacks
target specific applications

example:
- http flood
- login endpoint abuse

harder to detect

# Real soc indicators
- sudden spike in traffic
- same requests from multiple ips
- high cpu/memory usage
- increased latency
- service downtime

# DDos mitigation
- rate limiting
- web application firewall (WAF)
- CDN (cloudflare, akamai)
- Traffic filtering
- load balancing
- ip blocking

# MITM vs DDoS (important for interview)
| feature | MITM | DDoS |
|---------|------|------|
|goal |intercept data |disrupt service |
|impact |data theft |service outage |
|visibility |stealthy |noisy |
|detection |harder |easier |
|type |confidentiality attack |availability attack |

# soc analyst thinking
if you see:
- suspicious certificate warning
- users complaining about login
- dns mismatch

think it as MITM

if you see:
- website down
- traffic spike
- server overload

think it as ddos

