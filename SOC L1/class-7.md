# phishing and social engineering

what is phishing?
phishing is a social engineering attack where attackers trick users into:
- revealing credentials
- clicking malicious links
- downloading malware
- transferring money
- installing remote access tools

it attacks human psychology, not just systems

# email phishing
how it works:

1. victim receives fake email

2. email looks legitimate (bank, microsoft, courier,etc)

3. contains:
- malicious link
- fake login page
- infected attachment

4. user interacts

5. credentials stolen or malware installed

common tactics:
- your account will be suspended
- invoice attached
- click to reset password 
- salary increment details
- courier delivery failed

soc detection indicators:
- email from spoofed domain
- domain looks similar(micr0soft.com)
- suspicious attachments (.zip, .html, .exe, .docm)
- url redirect chains
- SPF(sender policy framework)/DKIM(domainkeys identified mail)/DMARC (domain-based message authentication, reporting and conformance) failure

# spear phishing
targeted phishing against a specific person or organization.
attacker researches:
- linkedin
- company website
- social media
- employees

example:
- attacker emails HR:
    "hi, this is the CFO. please transfer $5000 urgently"

this is also called business email compromise (BEC)

why its dangerous:
- looksextremely legitimate
- often bypasses spam filters
- high financial damage


# whaling
phishing targeting high level executives(ceo, cfo, directors)

high reward, high impact

# smishing and vishing
smishing:
phishing via sms.

example:
" your bank account blocked. click here"

vishing:
voice phishing via phone call.

example:
" i am from bank fraud department. tell me your otp"

# pharming
what is pharming?
pharming is an attack where the victim is redirected to a fake website even if they type the correct website address

unlike phishing:
- phishing -> user clicks malicious link
- pharming -> redirection happens silently

# method 1 - DNS poisoning

attacker compromises:
- dns server or local router

when user types:
- www.bank.com

dns returns:
- attacker ip address

user lands on fake site

# method 2 - hosts file modification
malware edits:
c:\windows\system32\drivers\etc\hosts

example:
192.168.1.200 www.bank.com
now user is redirected locally

why pharming is dangerous
- no suspicious email
- no obvious link
- looks like real domain
- harder for users to detect

soc detection indicators:
- sudden dns record changes
- suspicious dns responses
- internal dns anomalies
- multiple users resolving same domain to unusual ip
- host file modification alerts
- certificate mismatch errors

Real soc scenario
alert:
    multiple users accessing bank.com resolving to foreign ip.

investigation:
- check dns logs
- compare with known legitimate ip
- check for dns server compromise
- check endpoint for hosts file tampering

# Evil twin attack
what is evil twin?
- an attacker creates a fake wifi access point that looks identical to a legitimate one

example:
real wifi = cafe_wifi

attacker creates = cafe_wifi_free
- user connect unknowingly

how evil twin works
- attacker sets up rogue access point
- victim connects
- attacker intercepts traffic
- credentials captured
- session hijacking possible

this often leads to:
- MITM
- credential theft
- cookie stealing
- fake captive portal login pages

why it's dangerous 
- very easy to execute
- no technical skill required
- common in: airports, hotels, cafes, conferences

soc detection indicators:
inside corporate environment:
- unauthorized access point detected
- duplicate SSID detected
- arp spoofing alerts
- unusual dhcp server detected
- network traffic interception patterns

enterprise soc teams use:
- wireless IDS(WIDS)
- network access control (NAC)
- certificate based wifi auth (802. 1x)

# what is social engineering?
social engineering = psychological manipulation to trick people into:
- revealing sensitive info
- granting access
- perfroming security breaking actions
- installing malware
- transferring money

it exploits human vulnerabilities, not technical vulnerabilities

# core psychological attacks used by attackers
1. Authority
People obey authority figures.

Example:
“This is IT department. Share your password for system maintenance.”

Why it works:
Humans are conditioned to obey authority.

2. Urgency
Removes logical thinking.
“Your account will be deleted in 10 minutes.”
Victim panics → clicks immediately.

3. Fear
“Income tax notice attached.
Fear disables rational analysis.

4. Scarcity
“Only 2 bonus slots remaining.”
Triggers impulsive decisions.

5. Reciprocity
“I helped you last week, can you send me this document?”
Creates obligation.

6. Familiarity & Trust
Attackers often:
● Impersonate colleagues
● Use internal language
● Reference real project

# types of social engineering attacks
1. pretexting
attacker creates a fake scenario (pretext) to gain trust

example:
"hi, im from IT. we're upgrading vpn. please confirm your credentials

this is planned and researched

top seven pretexting attack techniques:
- 1. impersonation
- 2. tailgating 
- 3. piggybacking
- 4. baiting 
- 5. phishing 
- 6. vishing
- 7. scareware

2. baiting
attacker offers something tempting
example:
- free movie download
- free cracked software
- usb labeled "salary data"

curiosity + greed = compromise

3. watering hole attack
attacker compromise a website frequently visited by target group

example:
- government employees frequently visit specific portal
- attacker injects malware into that site

# social engineering attack lifecycle
1. reconnaissance
- linkedin
- company website
- social media

2. relationship building
- email conversation
- phone call

3. exploitation
- credentials
- file execution
- access granted

4. exit
- delete traces
- begin technical attack

# soc analyst perspective
As SOC L1, you usually see:
● Suspicious login after phishing
● VPN login from new location
● Email forwarding rules created
● MFA reset request
● Multiple password reset attempts
● Impossible travel login

# social engineering in indian context
● Fake GST notices
● Fake income tax emails
● Fake courier delivery scams
● KYC verification fraud
● Bank OTP scams
● Fake job offer scams

Many SOC alerts relate to:
● Credential harvesting
● OTP compromise
- account takeover

How Organizations Defend
● Security awareness training
● Phishing simulation campaigns
● Email filtering
● MFA enforcement
● Domain monitoring
● Zero trust approach
