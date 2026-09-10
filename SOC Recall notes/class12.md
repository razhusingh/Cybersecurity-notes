# SOC Analyst L1 – Day 12 

# 30-Second Recall
- MITM = Man-in-the-Middle Attack
- MITM = User ⇄ Attacker ⇄ Server
- Goal = Intercept & Modify Communication
- MITM Goals = Credential Theft, Cookie Theft, Data Modification, Malware Injection, Monitoring
- ARP Spoofing = Fake Router
- DNS Spoofing = Fake DNS Response
- SSL Stripping = HTTPS → HTTP
- Session Hijacking = Steal Session Cookie
- Evil Twin = Fake Wi-Fi Access Point
- MITM Indicators = ARP Changes, Duplicate MAC, SSL Warning, DNS Mismatch
- MITM Prevention = HTTPS, VPN, DNSSEC, Certificate Validation, WPA3
- DDoS = Distributed Denial of Service
- Goal = Make Service Slow or Unavailable
- DDoS Types = Volumetric, Protocol, Application Layer
- Volumetric = UDP Flood, ICMP Flood
- Protocol = SYN Flood, Ping of Death
- Application = HTTP Flood, Login Endpoint Abuse
- DDoS Indicators = Traffic Spike, High CPU, Latency, Downtime
- DDoS Mitigation = Rate Limiting, WAF, CDN, Load Balancer, IP Blocking
- MITM = Confidentiality Attack
- DDoS = Availability Attack

#  Must Remember Points
MITM (Man-in-the-Middle Attack)
Definition
- A MITM attack occurs when an attacker secretly intercepts communication between a user and a server.

Normal Communication
```
User
   │
Server
```
MITM
```
User
   │
Attacker
   │
Server
```
# Goals of MITM
- Steal Credentials
- Capture Session Cookies
- Modify Data in Transit
- Inject Malware
- Monitor Sensitive Communication

# Types of MITM Attacks
1. ARP Spoofing ⭐ (Most Important)

Attacker pretends to be the router.

Flow
```
Victim
   │
Attacker
   │
Router
   │
Internet
```

SOC Indicators
- Duplicate MAC Address
- ARP Table Changes
- Sudden Traffic Rerouting
- Internal Network Anomalies

2. DNS Spoofing
Attacker redirects a legitimate domain to a malicious IP.

Example
```
google.com

↓

Fake Server
```
Very similar to Pharming.

3. SSL Stripping
Attacker downgrades
```
HTTPS

↓

HTTP
```
User believes the website is secure, but communication is unencrypted.

4. Session Hijacking
Attacker steals the victim's session cookie.

Flow
```
User Login

↓

Cookie Created

↓

Cookie Stolen

↓

Attacker Logs In
```
No password required after stealing the cookie.

5. Evil Twin
Attacker creates a fake Wi-Fi hotspot.

Victim connects to it.

Entire traffic passes through the attacker.

# Real SOC Scenario (MITM)
Possible Alerts
- Multiple users using the same Gateway IP
- SSL Certificate Mismatch
- Suspicious DNS Responses

Investigation
- Check ARP Table
- Check DNS Logs
- Analyze Network Traffic
- Verify SSL Certificate
- Check Firewall/Proxy Logs

MITM Prevention
- HTTPS (TLS Encryption)
- VPN
- DNSSEC
- Certificate Validation
- Network Segmentation
- WPA3 Wi-Fi Security

# DDoS (Distributed Denial of Service)
Definition
- A DDoS attack floods a target with massive traffic to make it:
- Slow
- Unresponsive
- Completely Down

Goals of DDoS
- Take Website Offline
- Disrupt Business Operations
- Extortion
- Divert Attention from Other Attacks

Real SOC Scenario (DDoS)
Alert

Traffic increased:
```
2,000 req/sec

↓

200,000 req/sec
```
Source
- Multiple Countries

Target
- /login Endpoint

Likely Attack
- Application Layer DDoS

Types of DDoS Attacks
1. Volumetric Attack

Goal

Consume Network Bandwidth

Examples
- UDP Flood
- ICMP Flood

2. Protocol Attack

Goal

Consume Server Resources

Examples
- SYN Flood
- Ping of Death

3. Application Layer Attack

Goal

Target Specific Applications

Examples
- HTTP Flood
- Login Endpoint Abuse

Hardest DDoS type to detect.

DDoS Indicators
- Sudden Traffic Spike
- Same Requests from Multiple IPs
- High CPU Usage
- High Memory Usage
- Increased Latency
- Service Downtime

DDoS Mitigation
- Rate Limiting
- Web Application Firewall (WAF)
- CDN (Cloudflare / Akamai)
- Traffic Filtering
- Load Balancing
- IP Blocking

MITM vs DDoS
| MITM                     | DDoS                |
| ------------------------ | ------------------- |
| Intercepts Communication | Disrupts Service    |
| Data Theft               | Service Outage      |
| Stealthy                 | Noisy               |
| Harder to Detect         | Easier to Detect    |
| Confidentiality Attack   | Availability Attack |

# SOC Analyst Mindset
MITM Investigation Workflow
```
User Reports / Security Alert
        │
        ▼
Identify Symptoms
(SSL Warning / DNS Mismatch / Login Hijack)
        │
        ▼
Check Network Logs
        │
        ▼
Review ARP Table
        │
        ▼
Review DNS Logs
        │
        ▼
Verify SSL Certificate
        │
        ▼
Analyze Network Traffic
        │
        ▼
Determine Impact
        │
        ▼
Contain Attack
        │
        ▼
Escalate / Close
```
During MITM Investigation Ask Yourself
- Is there an SSL certificate mismatch?
- Has the DNS response changed?
- Is the ARP table modified?
- Are duplicate MAC addresses present?
- Are users reporting login/session hijacking?
- Is traffic passing through an unknown device?
- Has any sensitive data been intercepted?

# DDoS Investigation Workflow
```
Traffic Spike Alert
        │
        ▼
Validate Alert
        │
        ▼
Check Traffic Volume
        │
        ▼
Identify Attack Type
(Volumetric / Protocol / Application)
        │
        ▼
Analyze Source IPs
        │
        ▼
Check CPU / Memory / Latency
        │
        ▼
Identify Target Service
        │
        ▼
Apply Mitigation
(WAF / CDN / Rate Limit)
        │
        ▼
Escalate if Required
```
During DDoS Investigation Ask Yourself
- Has traffic increased suddenly?
- Which service is affected?
- Which attack type is being used?
- Are requests coming from multiple countries?
- Is CPU or memory usage unusually high?
- Is the website still available?
- Should mitigation be enabled immediately?

# Interview Q&A
Q1. What is a MITM attack?
-  A Man-in-the-Middle attack occurs when an attacker secretly intercepts communication between a user and a server.

Q2. What are the goals of a MITM attack?
- Steal credentials
- Capture session cookies
- Modify transmitted data
- Inject malware
- Monitor sensitive communication

Q3. Name five types of MITM attacks.
- ARP Spoofing
- DNS Spoofing
- SSL Stripping
- Session Hijacking
- Evil Twin

Q4. What is ARP Spoofing?
- An attacker pretends to be the router, causing traffic to pass through the attacker's system.

Q5. What is DNS Spoofing?
- Redirecting users to a fake IP address by manipulating DNS responses.

Q6. What is SSL Stripping?
- Downgrading HTTPS to HTTP so communication is no longer encrypted.

Q7. What is Session Hijacking?
- Stealing a user's session cookie to gain access without knowing the password.

Q8. What is an Evil Twin attack?
- A fake Wi-Fi access point created to intercept user traffic.

Q9. What is DDoS?
- A Distributed Denial of Service attack overwhelms a system with massive traffic, making it slow or unavailable.

Q10. Name the three major types of DDoS attacks.
- Volumetric
- Protocol
- Application Layer

Q11. Difference between MITM and DDoS?
- MITM targets confidentiality by intercepting communication.
- DDoS targets availability by overwhelming services with traffic.

# Question Paper Mode
1. What is a MITM attack?

2. What are the goals of MITM?

3. Explain ARP Spoofing.

4. Explain DNS Spoofing.

5. Explain SSL Stripping.

6. Explain Session Hijacking.

7. What is an Evil Twin attack?

8. What SOC indicators suggest a MITM attack?

9. How can a MITM attack be prevented?

10. What is a DDoS attack?

11. What are the goals of DDoS?

12. Name the three major types of DDoS attacks.

13. Give examples of Volumetric attacks.

14. Give examples of Protocol attacks.

15. Give examples of Application Layer attacks.

16. What SOC indicators suggest a DDoS attack?

17. How can DDoS attacks be mitigated?

18. Differentiate between MITM and DDoS.

19. Explain the MITM investigation workflow.

20. Explain the DDoS investigation workflow.

# Answer Key

1. An attacker secretly intercepts communication between a user and a server.

2. 
- Steal credentials
- Capture session cookies
- Modify transmitted data
- Inject malware
- Monitor communication

3. ARP Spoofing tricks devices into believing the attacker is the router.

4. DNS Spoofing redirects a legitimate domain to a malicious IP address.

5. SSL Stripping downgrades HTTPS connections to HTTP.

6. Session Hijacking steals session cookies to gain unauthorized access.

7. An Evil Twin is a fake Wi-Fi hotspot created by an attacker.

8.
- SSL certificate mismatch
- Duplicate MAC addresses
- ARP table changes
- DNS mismatch
- Network anomalies

9.
- HTTPS
- VPN
- DNSSEC
- Certificate Validation
- WPA3
- Network Segmentation

10. A DDoS attack floods a target with traffic to make it unavailable.

11.
- Take websites offline
- Disrupt business operations
- Extortion
- Diversion for other attacks

12.
- Volumetric
- Protocol
- Application Layer

13.
- UDP Flood
- ICMP Flood

14.
- SYN Flood
- Ping of Death

15.
- HTTP Flood
- Login Endpoint Abuse

16.
- Sudden traffic spike
- Same requests from multiple IPs
- High CPU usage
- Increased latency
- Service downtime

17.
- Rate Limiting
- WAF
- CDN
- Traffic Filtering
- Load Balancing
- IP Blocking

18.
|MITM | DDoS |
|-----|------|
|Data interception	|Service disruption |
|Confidentiality attack |Availability attack |
|Stealthy	|Noisy |
|Harder to detect	|Easier to detect |

19.
- Alert → Check ARP/DNS/SSL → Analyze Traffic → Determine Impact → Contain → Escalate/Close.

20.
- Traffic Spike → Validate → Identify Attack Type → Analyze Sources → Apply Mitigation → Escalate.