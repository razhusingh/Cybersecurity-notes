# SOC Analyst L1 – Day 14 
Protocols + Computer Ports

#  30-Second Recall
- Protocol = Rules for network communication

- HTTP = 80, web traffic, plaintext/stateless

- HTTPS = 443, HTTP + TLS encryption

- HTTP Methods = GET fetch, POST send, PUT update, DELETE remove, PATCH partial update

- Status Codes = 1xx Info, 2xx Success, 3xx Redirect, 4xx Client Error, 5xx Server Error

- HTTP is Stateless → Cookies/Sessions/Tokens maintain state

- DNS = 53, Domain → IP, mostly UDP

- DNS Resolution = Cache → Resolver → Root → TLD → Authoritative

- FTP = 21, File Transfer, plaintext

- SFTP = 22, File Transfer over SSH, encrypted

- SMTP = 25/587, Email Sending

- SSH = 22, Secure Remote Login

- RDP = 3389, Windows Remote Desktop

- SMB = 445, Windows File Sharing

- Port = Virtual endpoint identifying a network service/process

- Port Range = 0–65535

- Well-known = 0–1023

- Registered = 1024–49151

- Dynamic/Private = 49152–65535

- 21 FTP | 22 SSH/SFTP | 25 SMTP | 53 DNS | 80 HTTP | 443 HTTPS | 445 SMB | 3389 RDP

- 500 failed attempts on 3389 → Think RDP Brute Force

#  Must Remember
🌐 HTTP — Port 80

HTTP = Hypertext Transfer Protocol
- Transfers web content
- Client Request → Server Response
- Stateless = HTTP itself doesn't remember previous requests/user state
- Cookies, Sessions & Tokens maintain state

Methods
| Method | Purpose        |
| ------ | -------------- |
| GET    | Fetch          |
| POST   | Send/Create    |
| PUT    | Update/Replace |
| DELETE | Remove         |
| PATCH  | Partial Update |

status codes
- 1xx → Information
- 2xx → Success
- 3xx → Redirection
- 4xx → Client Error
- 5xx → Server Error

Remember: 200 OK, 301 Redirect, 400 Bad Request, 401 Unauthorized, 403 Forbidden, 404 Not Found, 500 Server Error

SOC: Suspicious URLs, repeated /login, unusual User-Agent, large POST → think web attack/brute force/exfiltration.

# 🔐 HTTPS — Port 443

HTTPS = HTTP + TLS encryption

Provides:
- Confidentiality
- Integrity
- Authentication

Without HTTPS → plaintext sniffing/MITM risk.

# 🌍 DNS — Port 53

DNS = Domain Name System

Domain Name → IP Address

Example: google.com → IP

Mostly uses UDP 53.

Resolution

Cache → Resolver → Root → TLD → Authoritative

SOC: Many DNS requests, suspicious/random domains/subdomains → think DNS Spoofing, DNS Tunneling, DGA.

# 📁 FTP vs SFTP

FTP — 21
- File Transfer
- Plaintext
- Active/Passive modes

SFTP — 22
- Runs over SSH
- Encrypted

SOC: Large transfers, unknown uploads, anonymous login → investigate exfiltration, brute force, credential exposure.

# 📧 SMTP — 25 / 587

SMTP = Email Sending
- 25 → SMTP/server-to-server commonly
- 587 → Message submission

SOC: Bulk emails, unknown sender domains, spoofing → think Phishing / Spam / Email Spoofing.

# 🔑 SSH — Port 22

SSH = Secure Shell

→ Secure remote login.

SOC: Failed logins, unusual IP, root-login attempts → think Brute Force / Credential Theft / Unauthorized Access.

# 🖥️ RDP — Port 3389

RDP = Remote Desktop Protocol

→ Remote access/control of Windows.

SOC: Odd-hour login, repeated attempts, external IP → think Brute Force / Lateral Movement / possible ransomware entry.

# 📂 SMB — Port 445

SMB = Server Message Block

→ Windows file sharing.

SOC: C$ admin-share access, unusual file movement → think Lateral Movement / SMB Relay / exploitation.

# 🔢 Computer Ports

A port is a virtual endpoint used to identify network services/processes.

Port Ranges
| Range       | Type            |
| ----------- | --------------- |
| 0–1023      | Well-known      |
| 1024–49151  | Registered      |
| 49152–65535 | Dynamic/Private |

⭐ Ports You MUST Know
- 21 FTP
- 22 SSH/SFTP
- 25 SMTP
- 53 DNS
- 80 HTTP
- 443 HTTPS
- 445 SMB
- 3389 RDP

# SOC example:

External IP → Internal Host → Port 3389 → 500 Failed Attempts

Your immediate thought:

🚨 RDP Brute Force

# Interview Q&A

Q1. What is a network protocol?
- A set of rules that defines how devices send and receive data.

Q2. HTTP vs HTTPS?
- HTTP uses 80 and is unencrypted. HTTPS uses 443 and protects communication using TLS.

Q3. What does HTTP stateless mean?
- HTTP itself doesn't remember previous requests. Cookies, sessions and tokens help maintain state.

Q4. Important HTTP methods?
- GET = Fetch, POST = Send/Create, PUT = Update/Replace, DELETE = Remove, PATCH = Partial Update.

Q5. Explain HTTP status-code classes.
- 1xx Information, 2xx Success, 3xx Redirect, 4xx Client Error, 5xx Server Error.

Q6. What is DNS?
- DNS resolves domain names → IP addresses, commonly using port 53.

Q7. Explain DNS resolution briefly.
- Cache → Resolver → Root → TLD → Authoritative server.

Q8. FTP vs SFTP?
- FTP = Port 21, plaintext. SFTP = Port 22, encrypted over SSH.

Q9. What is SMTP?
- Protocol for sending email. Common ports: 25 and 587.

Q10. What are SSH, RDP and SMB used for?
- SSH 22 = secure remote login; RDP 3389 = Windows remote desktop; SMB 445 = Windows file sharing.

# SOC Analyst Mindset
```
Alert
  ↓
Which Protocol?
  ↓
Which Port?
  ↓
Is activity normal for that service?
  ↓
Check Source → Destination
  ↓
Check Frequency / Volume / Time
  ↓
Identify suspicious behaviour
  ↓
Correlate Logs
  ↓
Close / Escalate
```
Quick thinking:
- 80/443 + suspicious URL → Web attack?
- 53 + random subdomains → DNS tunnelling/DGA?
- 21 + huge outbound transfer → Data exfiltration?
- 25/587 + bulk emails → Spam/phishing?
- 22 + repeated failures → SSH brute force?
- 3389 + repeated failures → RDP brute force?
- 445 + unusual C$ access → Lateral movement?

soc example
```
Source: External IP
Destination: Internal Host
Port: 3389
Attempts: 500
Status: Failed
```
Immediate hypothesis → RDP brute-force activity. Then validate with surrounding logs/context before confirming.

# Question Paper Mode

1. What is a network protocol?

2. Differentiate HTTP and HTTPS, including their ports.

3. What does HTTP being stateless mean, and how is state maintained?

4. Explain GET, POST, PUT, DELETE and PATCH.

5. Explain the five HTTP status-code classes and important examples.

6. What is DNS, which port does it use, and what does it resolve?

7. Explain the DNS resolution process.

8. Name important DNS attack indicators and attacks.

9. Differentiate FTP and SFTP, including ports.

10. What suspicious FTP activity should a SOC analyst investigate?

11. What is SMTP? Name its important ports and security concerns.

12. What is SSH? What suspicious SSH activity might indicate an attack?

13. What is RDP? What suspicious RDP activity should a SOC analyst recognise?

14. What is SMB? What suspicious SMB activity can indicate lateral movement?

15. What is a computer port?

16. Explain Well-known, Registered and Dynamic/Private port ranges.

17. Give the protocols/services for ports 21, 22, 25, 53, 80, 443, 445 and 3389.

18. An external IP makes 500 failed connections to port 3389. What attack would you suspect?

# Answer Key

1. Rules defining how network devices communicate.

2. HTTP = 80, unencrypted; HTTPS = 443, TLS-protected.

3. HTTP doesn't inherently remember previous requests; cookies, sessions and tokens help maintain state.

4. GET = Fetch; POST = Send/Create; PUT = Update/Replace; DELETE = Remove; PATCH = Partial Update.

5. 1xx = Information, 2xx = Success, 3xx = Redirect, 4xx = Client Error, 5xx = Server Error. Examples: 200, 301, 400, 401, 403, 404, 500.

6. DNS maps domain names to IP addresses; port 53, commonly UDP.

7. Cache → Resolver → Root → TLD → Authoritative.

8. Indicators: excessive DNS requests, suspicious/random domains/subdomains. Attacks: DNS Spoofing, DNS Tunnelling, DGA.

9. FTP = 21, plaintext; SFTP = 22, encrypted over SSH.

10. Large file transfers, unknown uploads and anonymous logins.

11. SMTP sends email; 25/587. Watch for bulk sending, spoofing, phishing and spam.

12. SSH = secure remote login on 22. Repeated failed logins, unusual IPs and root-login attempts are suspicious.

13. RDP = Windows remote desktop on 3389. Repeated attempts, external-IP logins and odd-hour access are suspicious.

14. SMB = Windows file sharing on 445. Unusual admin-share access/file movement can indicate lateral movement.

15. A virtual endpoint associated with a network service/process.

16.
- 0–1023 = Well-known
- 1024–49151 = Registered
- 49152–65535 = Dynamic/Private

17. 21 FTP | 22 SSH/SFTP | 25 SMTP | 53 DNS | 80 HTTP | 443 HTTPS | 445 SMB | 3389 RDP

18. Suspect RDP brute force, then investigate supporting context/logs.

