# DAY 7(1) — RAJU RECALL NOTES
## PHISHING & SOCIAL ENGINEERING

---

# 1. 30-SECOND RECALL

**Phishing = Social Engineering attack** that tricks users into:
- Revealing credentials
- Clicking malicious links
- Downloading malware
- Transferring money
- Installing remote-access tools

**Core idea:** Attacks **human psychology**, not only technical systems.

### Main Types
`Email Phishing → Spear Phishing → Whaling → Smishing → Vishing → Pharming`

### Other Social Engineering Attacks
`Pretexting → Baiting → Watering Hole`

:contentReference[oaicite:0]{index=0}

---

# 2. MUST REMEMBER

## 📧 Email Phishing

### Flow
`Fake Email → User interacts → Credential theft / Malware installation`

Common lures:
- Account suspension
- Invoice attachment
- Password reset
- Salary increment
- Failed courier delivery

### SOC Indicators
- Spoofed sender/domain
- Look-alike domain → `micr0soft.com`
- Suspicious `.zip / .html / .exe / .docm`
- URL redirect chains
- SPF/DKIM/DMARC failure

:contentReference[oaicite:1]{index=1}

---

## 🎯 Spear Phishing

**Targeted phishing** against a specific person/organization.

Attacker researches:
`LinkedIn + Company Website + Social Media + Employees`

Example: Fake CFO asks HR to urgently transfer money.

**Also called:** Business Email Compromise (BEC)

**Danger:** Highly believable + may bypass spam filters + financial damage.

:contentReference[oaicite:2]{index=2}

---

## 🐋 Whaling

Phishing targeting **high-level executives**:
`CEO / CFO / Directors`

**High reward → High impact**

:contentReference[oaicite:3]{index=3}

---

## 📱 Smishing vs Vishing

| Type | Method |
|---|---|
| **Smishing** | Phishing via SMS |
| **Vishing** | Voice phishing via phone |

Example:
- Smishing → fake bank SMS + malicious link
- Vishing → fake bank caller asks for OTP

:contentReference[oaicite:4]{index=4}

---

# 3. PHARMING

**Pharming = Victim silently redirected to fake website even after typing the correct address.**

### Key Difference

| Phishing | Pharming |
|---|---|
| User clicks malicious link | Redirection happens silently |
| Usually email/message based | DNS/host manipulation can cause redirect |

:contentReference[oaicite:5]{index=5}

### Method 1 — DNS Poisoning

`Compromise DNS server/router → User enters bank.com → DNS returns attacker IP → Fake site`

:contentReference[oaicite:6]{index=6}

### Method 2 — Hosts File Modification

Malware modifies:

`C:\Windows\System32\drivers\etc\hosts`

Example:

`192.168.1.200 www.bank.com`

**Why dangerous?**
- No suspicious email
- No obvious link
- Looks like real domain
- Hard for user to notice

:contentReference[oaicite:7]{index=7}

### SOC Indicators
- Sudden DNS record changes
- Suspicious DNS responses
- Internal DNS anomalies
- Multiple users → same domain → unusual IP
- Hosts-file modification alerts
- Certificate mismatch

### Investigation
`DNS Logs → Compare legitimate IP → Check DNS server → Check hosts file`

:contentReference[oaicite:8]{index=8}

---

# 4. EVIL TWIN ATTACK

**Evil Twin = Fake Wi-Fi AP made to look like a legitimate Wi-Fi network.**

Example:
`Real: Cafe_WiFi`
`Fake: Cafe_WiFi_Free`

### Attack Flow
`Rogue AP → Victim connects → Traffic intercepted → Credentials captured → Possible session hijacking`

Can lead to:
- MITM
- Credential theft
- Cookie stealing
- Fake captive portal

:contentReference[oaicite:9]{index=9}

### SOC Indicators
- Unauthorized AP
- Duplicate SSID
- ARP spoofing alerts
- Unusual DHCP server
- Traffic interception patterns

### Enterprise Defense
- WIDS
- NAC
- Certificate-based Wi-Fi authentication → **802.1X**

Common locations:
`Airports / Hotels / Cafes / Conferences`

:contentReference[oaicite:10]{index=10}

---

# 5. SOCIAL ENGINEERING

**Social Engineering = Psychological manipulation used to make people:**
- Reveal sensitive information
- Grant access
- Perform security-breaking actions
- Install malware
- Transfer money

**Key idea:** Exploits **human vulnerabilities**, not technical vulnerabilities.

:contentReference[oaicite:11]{index=11}

---

# 6. PSYCHOLOGICAL TRIGGERS

| Trigger | Effect |
|---|---|
| **Authority** | People obey authority |
| **Urgency** | Removes logical thinking |
| **Fear** | Disables rational analysis |
| **Scarcity** | Causes impulsive decisions |
| **Reciprocity** | Creates obligation |
| **Familiarity/Trust** | Lowers suspicion |

### Familiarity tricks
Attackers may:
- Impersonate colleagues
- Use internal language
- Reference real projects

:contentReference[oaicite:12]{index=12}

---

# 7. TYPES OF SOCIAL ENGINEERING

## 🎭 Pretexting
Attacker creates a **fake scenario/pretext** to gain trust.

Example:
> Fake IT employee asks for VPN credentials.

**Key:** Planned + researched.

:contentReference[oaicite:13]{index=13}

---

## 🎁 Baiting

Attacker offers something **tempting**.

Examples:
- Free movie
- Cracked software
- USB labelled “Salary Data”

**Formula:** `Curiosity + Greed → Compromise`

:contentReference[oaicite:14]{index=14}

---

## 💧 Watering Hole

Attacker compromises a website **frequently visited by the target group**.

Example:
`Target employees visit portal → Attacker compromises portal → Malware delivered`

**Key:** Very targeted.

:contentReference[oaicite:15]{index=15}

---

# 8. SOCIAL ENGINEERING ATTACK LIFECYCLE

| Stage | What Happens |
|---|---|
| **1. Reconnaissance** | LinkedIn, company website, social media |
| **2. Relationship Building** | Email / phone interaction |
| **3. Exploitation** | Credentials, file execution, access |
| **4. Exit** | Delete traces OR begin technical attack |

:contentReference[oaicite:16]{index=16}

---

# 9. SOC ANALYST PERSPECTIVE

SOC L1 commonly sees:

- Suspicious login after phishing
- VPN login from new location
- New email-forwarding rules
- MFA reset request
- Multiple password-reset attempts
- Impossible-travel login

**Think:**  
`Phishing → Credential Theft → Account Takeover → Suspicious Login`

:contentReference[oaicite:17]{index=17}

---

# 10. INDIAN CONTEXT 🇮🇳

Common examples:
- Fake GST notices
- Fake Income Tax emails
- Fake courier scams
- KYC verification fraud
- Bank OTP scams
- Fake job offers

Common SOC consequences:
`Credential Harvesting + OTP Compromise + Account Takeover`

:contentReference[oaicite:18]{index=18}

---

# 11. ORGANIZATIONAL DEFENSE

- Security awareness training
- Phishing simulation campaigns
- Email filtering
- MFA enforcement
- Domain monitoring
- Zero Trust approach

:contentReference[oaicite:19]{index=19}

---

# 12. SOC ANALYST MINDSET

When a phishing/social-engineering alert appears, ask:

1. **Who was targeted?**
2. **What psychological trick was used?**
3. **Was a link/attachment involved?**
4. **Were credentials exposed?**
5. **Was MFA reset/bypassed?**
6. **Did the user log in from a new/impossible location?**
7. **Were forwarding rules created?**
8. **Is there account takeover?**
9. **Is malware execution happening?**
10. **Did the attack move from social engineering to a technical attack?**

---

# 13. INTERVIEW Q&A

### Q1. What is phishing?
A social-engineering attack that tricks users into performing malicious actions.

### Q2. Phishing vs spear phishing?
Phishing is broad; spear phishing is specifically targeted and researched.

### Q3. What is whaling?
Phishing targeting executives such as CEO/CFO.

### Q4. Smishing vs vishing?
SMS phishing vs phone/voice phishing.

### Q5. Phishing vs pharming?
Phishing tricks the user into clicking; pharming silently redirects the user.

### Q6. What is DNS poisoning?
Manipulating DNS resolution so a legitimate domain resolves to an attacker-controlled IP.

### Q7. What is Evil Twin?
A fake Wi-Fi AP designed to imitate a legitimate network.

### Q8. What is pretexting?
Creating a believable fake scenario to gain trust/access.

### Q9. What is baiting?
Using something tempting to make the victim compromise security.

### Q10. What is a watering hole?
Compromising a website frequently visited by the target group.

### Q11. Name social-engineering psychological triggers.
Authority, urgency, fear, scarcity, reciprocity, familiarity/trust.

### Q12. What phishing-related alerts can SOC L1 see?
Suspicious login, new-location VPN login, MFA reset, password-reset attempts, forwarding rules, impossible travel.

---

# 14. QUESTION PAPER MODE

1. Define phishing.
2. What is the main target of social engineering?
3. Explain email phishing flow.
4. List common email-phishing SOC indicators.
5. What is spear phishing?
6. What is BEC?
7. What is whaling?
8. Smishing vs vishing?
9. Define pharming.
10. Phishing vs pharming?
11. Explain DNS-poisoning-based pharming.
12. Explain hosts-file-based pharming.
13. List SOC indicators of pharming.
14. What is an Evil Twin attack?
15. Explain the Evil Twin attack flow.
16. List Evil Twin SOC indicators and defenses.
17. Define social engineering.
18. Explain six psychological triggers.
19. What is pretexting?
20. What is baiting?
21. What is a watering-hole attack?
22. Explain the social-engineering lifecycle.
23. What alerts can SOC L1 see after social engineering?
24. Give examples of social-engineering scams in India.
25. How can organizations defend against social engineering?

---

# 15. ANSWER KEY

1. Social-engineering attack that tricks users into malicious actions.
2. Human psychology/vulnerabilities.
3. Fake email → interaction → credential theft/malware.
4. Spoofed domain, look-alike domain, suspicious attachment, redirects, SPF/DKIM/DMARC failure.
5. Targeted phishing.
6. Business Email Compromise.
7. Executive-targeted phishing.
8. SMS vs voice phishing.
9. Silent redirection to a fake website.
10. Phishing requires user interaction; pharming redirects silently.
11. DNS/router compromised → attacker IP returned → fake site.
12. Malware changes the hosts file to map legitimate domain to attacker IP.
13. DNS changes/anomalies, unusual IP resolution, hosts-file alerts, certificate mismatch.
14. Fake Wi-Fi AP imitating legitimate Wi-Fi.
15. Rogue AP → victim connects → interception → credential theft/session hijacking.
16. Unauthorized/duplicate AP, ARP spoofing, unusual DHCP; WIDS/NAC/802.1X.
17. Psychological manipulation of people.
18. Authority, urgency, fear, scarcity, reciprocity, familiarity/trust.
19. Fake scenario used to gain trust.
20. Tempting offer used to trigger compromise.
21. Compromising a frequently visited target-group website.
22. Recon → Relationship → Exploitation → Exit.
23. Suspicious login, new-location VPN, MFA reset, password resets, forwarding rules, impossible travel.
24. Fake GST/IT notices, courier, KYC, OTP, job offers.
25. Awareness, phishing simulations, email filtering, MFA, domain monitoring, Zero Trust.

---