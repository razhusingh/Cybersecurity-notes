# Soc analyst l1 day 14
# Protocols and computer ports

1. What Are Web Protocols?
- A protocol is a set of rules that defines how data is sent and received between devices over a network.

Simple idea:
- Humans communicate using languages.
- Computers communicate using protocols such as HTTP, HTTPS, DNS, FTP, SMTP, SSH, etc.
- Without protocols, devices would not understand how to communicate.

Protocols in the OSI Model
| Layer       | Examples              |
| ----------- | --------------------- |
| Application | HTTP, HTTPS, DNS, FTP |
| Transport   | TCP, UDP              |
| Network     | IP                    |
| Data Link   | Ethernet, Wi-Fi       |

⭐ Interview Important: HTTP, DNS, FTP etc. are application-layer protocols, while TCP/UDP handle transport.

2. HTTP — Hypertext Transfer Protocol
- HTTP is the main protocol used for communication between web clients (browsers) and web servers.

- Default port: TCP 80
- Data is not encrypted by HTTP itself.
- HTTP is stateless.

# How HTTP Works
Step 1 — Client Request
GET /index.html HTTP/1.1
Host: example.com
User-Agent: Chrome

Step 2 — Server Response
HTTP/1.1 200 OK
Content-Type: text/html

<html>...</html>

Basic flow:
```
Browser → HTTP Request → Server
Browser ← HTTP Response ← Server
```
When a browser accesses a website, it may first use DNS to obtain the server's IP, establish a connection, send the HTTP request, receive the response, and display the content.

3. HTTP Methods
- HTTP methods indicate what action the client wants to perform.
| Method | Purpose                     |
| ------ | --------------------------- |
| GET    | Fetch/retrieve data         |
| POST   | Send/submit data            |
| PUT    | Update/replace a resource   |
| DELETE | Remove a resource           |
| PATCH  | Partially update a resource |

⭐ Interview Important: Know the basic purpose of GET, POST, PUT, DELETE and PATCH.

4. Stateless Nature of HTTP
HTTP is stateless, meaning HTTP itself does not automatically remember:
- Who the user is.
- Previous requests.

Web applications therefore use:
- Cookies
- Sessions
- Tokens

to maintain user/application state.

Example:
```
Login → Session created → Cookie/token issued
                     ↓
Future requests identify the session
```
⭐ Interview Important: HTTP is stateless.

5. HTTP Status Codes
- HTTP status codes indicate what happened to a request.
| Range   | Meaning       |
| ------- | ------------- |
| 100–199 | Informational |
| 200–299 | Successful    |
| 300–399 | Redirection   |
| 400–499 | Client error  |
| 500–599 | Server error  |

important codes:
| Code | Meaning                      |
| ---: | ---------------------------- |
|  200 | OK                           |
|  301 | Redirect / Moved Permanently |
|  400 | Bad Request                  |
|  401 | Unauthorized                 |
|  403 | Forbidden                    |
|  404 | Not Found                    |
|  500 | Internal Server Error        |

⭐ Interview Important:
- 401 → authentication is required/invalid.
- 403 → server understands the request but access is forbidden.

6. HTTP — SOC Perspective
SOC Indicators

Watch for:
- Suspicious URLs.
- Repeated requests, especially /login.
- Unusual User-Agent values.
- Large or unusual POST requests.
- Abnormally high request volume.

Common Attacks
- XSS
- SQL Injection
- Credential harvesting
- HTTP Flood / DDoS

Example:
```
POST /login → Failed
POST /login → Failed
POST /login → Failed
...
```
Many repeated login attempts may indicate brute force/password attacks.

Useful logs include:
- Web server logs
- WAF logs
- Proxy/reverse-proxy logs
- SIEM/IDS alerts

7. HTTPS — Secure HTTP
- HTTPS is HTTP protected using TLS encryption.

HTTPS → TCP Port 443

HTTPS provides:
- Confidentiality → data is encrypted.
- Integrity → helps prevent undetected modification.
- Authentication → certificates help verify the server.

Without HTTPS, plaintext traffic may expose sensitive data and be vulnerable to interception/MITM attacks.

⭐ Interview Important
```
HTTP  → Port 80  → Unencrypted
HTTPS → Port 443 → Encrypted using TLS
```
Correction: Modern HTTPS uses TLS. SSL is obsolete, although people still sometimes say “SSL certificate.”

8. DNS — Domain Name System
- DNS converts human-readable domain names into IP addresses.

Example:
- google.com → 142.250.x.x

DNS is often called the phonebook of the Internet.

Port
DNS → Port 53

DNS uses UDP 53 for most normal queries, but it can also use TCP 53.

⭐ Interview Important: DNS uses both UDP and TCP port 53; don't memorise it as UDP-only.

9. DNS Resolution Process
Simplified resolution:
```
User enters domain
      ↓
Browser cache
      ↓
OS cache
      ↓
DNS Resolver
      ↓
Root Server
      ↓
TLD Server
      ↓
Authoritative Server
      ↓
IP Address returned
```
Root Server
- Directs the resolver towards the correct TLD server.

TLD Server
Handles top-level domains such as:
- .com
- .net
- .org
- .edu

and points towards the appropriate authoritative server.

Authoritative DNS Server
- Provides authoritative DNS information for the requested domain.

⭐ Interview Important
```
Resolver → Root → TLD → Authoritative
```
Caching can mean not every query needs the entire process.

10. DNS — SOC Perspective
SOC Indicators

Watch for:
- Too many DNS requests.
- Suspicious domains.
- Random-looking domains/subdomains.
- Very long or unusual subdomains.
- DNS tunnelling patterns.

# DNS Attacks :

 DNS Spoofing
- An attacker causes incorrect DNS information to be returned, potentially redirecting a victim towards a malicious destination.

DNS Tunnelling
- DNS queries/responses are abused to transfer data or communicate with attacker infrastructure.

Can be used for:
- Data exfiltration.
- Command-and-control communication.

DGA — Domain Generation Algorithm
- Malware may automatically generate many domains such as:
```
xk29abc.com
qwe82xyz.net
```
and attempt to contact them until it finds attacker-controlled infrastructure.

SOC analysts should pay attention to random-looking domains and large numbers of failed DNS lookups.

11. FTP — File Transfer Protocol
- FTP transfers files between systems.
```
FTP → TCP Port 21
```
Traditional FTP sends credentials/data without encryption and is therefore not secure by default.

FTP has two modes:
- Active
- Passive

These mainly differ in how the data connection is established.

12. SFTP — SSH File Transfer Protocol
- SFTP securely transfers files over SSH.
SFTP → TCP Port 22

 - Traffic is encrypted.
- Uses SSH.

⭐ Interview Important
```
FTP  → Port 21 → Plaintext by default
SFTP → Port 22 → Encrypted using SSH
```
Correction: SFTP technically means SSH File Transfer Protocol, not simply “Secure FTP.” It is different from traditional FTP.

13. FTP/SFTP — SOC Perspective

SOC Indicators
- Large file transfers.
- Unknown/unexpected uploads.
- Anonymous FTP login.
- Unexpected external file transfers.
- Repeated failed logins.

Threats
- FTP credential sniffing.
- Data exfiltration.
- Brute-force login attempts.

During investigation, check:
```
Source/Destination IP
Username
Login result
Files transferred
File size
Transfer direction
Time
```
14. SMTP — Simple Mail Transfer Protocol
- SMTP is primarily used to send and relay email.

Important ports:
|Port |	Use |
|-----|-----|
|25	| SMTP / mail server relay |
|587 |	Email message submission|

Basic flow:
```
Sender → SMTP Server → Internet → Receiving Mail Server
```
SOC Indicators
- Bulk email sending.
- Unknown/suspicious sender domains.
- Email spoofing.
- Unusual outbound email volume.

Common Attacks
- Phishing
- Spam campaigns
- Email spoofing

SOC analysts commonly investigate sender information, sending IP, email headers, URLs and attachments.

15. SSH — Secure Shell
- SSH provides secure encrypted remote login/access.
SSH → TCP Port 22

SOC Indicators
- Multiple failed logins.
- Login from unusual IP addresses.
- Root login attempts.
- Successful login after many failures.
- Unexpected login times.

Common Attacks
- SSH brute force.
- Credential theft.
- Unauthorized access.

Example:
```
Failed login × 100
        ↓
Successful login
```
This should be investigated because the attacker may have successfully guessed/stolen credentials.

16. RDP — Remote Desktop Protocol
- RDP is mainly used for remote control/access of Windows systems.
RDP → Port 3389

SOC Indicators
- Login at unusual hours.
- Multiple login attempts.
- External IP login.
- Successful login after repeated failures.

Common Threats
- RDP brute force.
- Lateral movement.
- Ransomware-related initial access/activity.
⭐ Interview Important: RDP uses 3389 and exposed RDP is a common attack target.

17. SMB — Server Message Block
- SMB is commonly used for Windows file and resource sharing.
SMB → TCP Port 445

It can also be used to access administrative shares such as:
```
C$
ADMIN$
IPC$
```

SOC Indicators
- Unexpected access to C$.
- File movement between systems.
- Unusual port 445 connections.
- Possible lateral movement.

Common Attacks
- EternalBlue
- SMB Relay
- Lateral Movement
⭐ Interview Important: SMB commonly uses TCP 445.

18. What is a Computer Port?
A port is a logical/software-based communication endpoint used to identify which application or service should receive network traffic.

Example:

192.168.1.10:443

Here:
```
192.168.1.10 → IP address / host
443          → HTTPS service port
```
Different services can therefore communicate through the same computer using different ports.

19. Port Number Ranges
- Ports range from:
0–65535

They are divided into:
| Range       | Type                    |
| ----------- | ----------------------- |
| 0–1023      | Well-known/System Ports |
| 1024–49151  | Registered Ports        |
| 49152–65535 | Dynamic/Private Ports   |

Well-Known Ports

Used by common standard services.

Examples:
```
21  FTP
22  SSH
25  SMTP
53  DNS
80  HTTP
443 HTTPS
445 SMB
```
Registered Ports
Often associated with specific applications.

Examples:
```
1433 → Microsoft SQL Server
3306 → MySQL
3389 → RDP
```
Dynamic / Private Ports
- Usually used as temporary client-side ports.

Example:
```
Client: 192.168.1.5:52000
              ↓
Server: 93.x.x.x:443
```
52000 is the temporary client port while 443 is the HTTPS server port.

20. Internal vs External Ports
- The PDF also discusses internal and external ports.

Internal
- A service is reachable only inside the private network/LAN.

External
- A service is exposed/reachable through the Internet, often through firewall/NAT configuration.

Important clarification: internal/external ports are not separate official port-number ranges.

From a SOC perspective, externally exposed services such as RDP, SSH, SMB or databases deserve additional attention because they increase attack exposure.

21. Important Ports for SOC Analyst L1
⭐ Memorise these
|     Port | Protocol        | Purpose                            |
| -------: | --------------- | ---------------------------------- |
|   **21** | FTP             | File transfer                      |
|   **22** | SSH / SFTP      | Secure remote access/file transfer |
|   **25** | SMTP            | Email sending/relay                |
|   **53** | DNS             | Domain resolution                  |
|   **80** | HTTP            | Web traffic                        |
|  **443** | HTTPS           | Secure web traffic                 |
|  **445** | SMB             | Windows file sharing               |
|  **587** | SMTP Submission | Email submission                   |
| **3389** | RDP             | Remote desktop                     |

SOC Important Addition

Other useful ports to recognise:
| Port | Protocol |
| ---: | -------- |
|  110 | POP3     |
|  143 | IMAP     |
|  389 | LDAP     |
|  636 | LDAPS    |
| 1433 | MSSQL    |
| 3306 | MySQL    |

A port suggests the expected service, but it does not guarantee it. Services can be configured to use non-standard ports.

22. Real SOC Log Example

The final PDF example gives:
```
Source IP:      185.221.x.x
Destination IP: 192.168.1.10
Port:           3389
Attempts:       500
Status:         Failed
```
Analysis:
```
Port 3389
   ↓
RDP
   ↓
500 attempts
   ↓
All/mostly failed
   ↓
Possible RDP brute-force attack
```
As an L1 analyst, investigate:
- Source IP.
- Target system.
- Targeted username/account.
- Number and timing of attempts.
- Whether RDP should be exposed.
- Whether any authentication eventually succeeded.
- Whether the same IP targeted other systems.

# SOC Important Addition

Useful Windows authentication Event IDs:
```
4624 → Successful logon
4625 → Failed logon
```
These can help determine whether repeated login attempts eventually resulted in successful access.

23. Protocol → Threat Quick Understanding
|Protocol |	Main SOC Concerns |
|---------|-------------------|
|HTTP/HTTPS	|Web attacks, suspicious URLs, web traffic |
|DNS	|Tunnelling, DGA, malicious domains |
|FTP/SFTP	|Suspicious file transfer, exfiltration |
|SMTP	|Phishing, spam, spoofing |
|SSH	|Brute force, unauthorized access |
|RDP	|Brute force, lateral movement |
|SMB	|Lateral movement, file/admin-share abuse |

The key SOC principle is context.

For example:
```
Port 3389 alone
= Normal RDP traffic may be possible
```
But:
```
Unknown external IP
+ Port 3389
+ 500 login attempts
+ 500 failures
= Strong RDP brute-force indicator
```
Similarly:
```
One normal DNS query
= Normal
```
but:
```
Thousands of DNS queries
+ Random/long subdomains
+ Suspicious domain
= Possible DNS tunnelling/malware activity
```
So correlate:

- Protocol + Port + Source + Destination + Frequency + Time + Authentication Result + Normal Behaviour