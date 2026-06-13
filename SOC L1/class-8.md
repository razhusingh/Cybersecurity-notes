# Password & Credential Stuffing Attack For SOC

# types of password attacks
Brute force attack:
- a brute force attack is when an attacker tries many possword combinations repeatedly until the correct one works

attacker tries every possible password combination until one works
- try->fail->try->fail->try-> success

how it works:
- attacker targets login portal (vpn, RDP, Web app)
- sends thousands of password attempts
- if no account lockout -> eventually success

# soc indicators:
in windows logs:
- event id 4625(failed login)
- multiple attempts from same ip
- same username targeted repeatedly

in firewall/vpn
- high authentication failures
- login attempts at high frequency 

# real example
you see:
- 500 failed logins for user administrator
- from ip 185.x.x.x
- within 10 minutes

this is classic brute force

# types of brute force attacks
- 1. simple brute force attacks
- 2. dictionary attacks
- 3. hybrid brute force attacks
- 4. reverse brute force attacks
- 5. credential stuffing

uses automated tools:
- hydra
- burp suite
- medusa
- ncrack

# reverse bruteforce attack
instead of using many password for one user, attacker uses one password for many users

(similar to "password spraying" but usually focused on one known weak password like "summer2025")

often used when attacker believes. "company uses predictable pattern"

# dictionary attack
instead of trying all combinations, attacker uses a wordlist of common passwords
- password
- admin123 or admin or admin@123
- welcome123
- india@123

soc indicators:
- attempts follow common password pattern
- login attempts across many systems
- moderate speed attempts

# password spraying
concept: one password -> many users

instead of: admin -> 1000 attempts
attacker does: 1000 users -> welcome@123

why it works:
many employees use predictable corporate patterns:
- company@2025
- welcome@123
- p@ssword1

soc indicators:
- one password attempt per account
- spread over many usernames
- attempts spaced over time
- no lockout triggered

# hybrid attack
- combination of dictionary + variations, customized to target organization

example:
company@2023
company@2024
company@123

soc indicators;
- slight password variations
- targeted to company name

# rainbow table attack
what happens
- if attacker steals database containing: password hashes (md5, sha1 etc.)

they use precomputed rainbow tables to reverse hashes into plaintext passwords

soc may not directly see this, but DFIR team might during investigation

# credential stuffing
attackers use:
- previouslu leaked username/password combos from data breaches

example:
- user uses same password everywhere

if one website gets breached -> attacker tests same credentials 0n:
- email
- banking
- vpn
- corporate login

soc indicators
- login attempts from multiple ips
- valid username + valid password but unusual location
- impossible travel alerts
- high login success after many failures

# MFA fatigue attack
attacker:
- gets password
- tries to login repeatedly
- victim receives many MFA push notification
- victim clicks "approve" out of frustration

soc sees:
- multiple MFA requests
- followed by successful login

very common in azure ad environment

# about password attack
 where these attacks commonly target
- RDP (PORT 3389)
- SSH (PORT 22)
- VPN portals
- web applications 
- database login panels

Attack chain example(very real)
- 1. phishing email
- 2. credential stolen
- 3. attacker tries vpn
- 4. MFA enabled -> fails
- 5. attacker attempts password spary
- 6. finds weak service account
- 7. gains internal access

this is extermely common in ransomware cases

# soc l1 investigation workflow

When you get alert:
"Multiple failed login attempts"

You must check:
- Source IP
- Geo location
- Username targeted
- Success or only failures?
- Time frequency
- Account lockout triggered?
- Any successful login after failures?

If yes → escalate immediately.

 # important logs to master:

 Windows
- 4625 → Failed login
- 4624 → Successful login
- 4776 → NTLM authentication
- 4740 → Account lockout

 Linux
 - /var/log/auth.log
 - SSH login attempts

 Firewall
 - Repeated connection attempts
 - Blocked connection spikes
 
 # prevention mechanisms
 - acount lockout policy
 - MFA enforcement
 - rate limiting 
 - CAPTCHA
 - geo-blocking
 - strong password policy 
 - disable default accounts

 # Attack comparison
 | attack | speed | detection difficulty | common in soc |
 |--------|-------|----------------------|---------------|
 |brute force |high |easy |very common |
 |dictionary |medium |medium |common |
 |password spraying |low and slow |hard |very common |
 |credential stuffing |medium |hard |very common |
 |hybrid |medium |medium |common |
 |rainbow table |offline |hard |post-breach |
 |MFA fatigue |stealthy |hard |increasing |
