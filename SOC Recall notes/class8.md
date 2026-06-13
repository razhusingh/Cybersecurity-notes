# 🚀 30-Second Recall

# Brute Force Attack
- Many passwords → One user
- Tries every possible password

Indicators:
- Event ID 4625 spikes
- Same user targeted repeatedly
- Many failures from same IP

# Reverse Brute Force Attack
- One password → Many users
- Example:
Summer2025
Welcome@123

# Dictionary Attack
- Uses common password wordlists
- Faster than brute force
- Examples:
password
admin
welcome123

# Password Spraying
- One password → Many accounts
- Low and slow attack
- Avoids account lockout
- Very common in enterprises

# Hybrid Attack
- Dictionary + Custom variations
- Example:
Company@2024
Company@123

# Rainbow Table Attack
- Uses precomputed tables
- Cracks stolen password hashes
- Usually seen during DFIR investigations

# Credential Stuffing
- Uses leaked credentials from breaches
- Same password reused on multiple sites

Indicators:
- Impossible travel
- Unusual login location
- High success rate after failures

# MFA Fatigue Attack
- User receives many MFA prompts
- Victim eventually clicks Approve
- Common in Azure AD environments

# 🎯 Interview Questions
- Q1. What is Brute Force Attack?
A: Trying all possible password combinations until one works.

- Q2. Difference between Brute Force and Password Spraying?
Brute Force
Many passwords → One user
Password Spraying
One password → Many users

- Q3. What is Credential Stuffing?
A: Using leaked username/password combinations from previous breaches.

- Q4. What is MFA Fatigue?
A: Repeated MFA requests sent to victim until they approve login.

- Q5. What is Rainbow Table Attack?
A: Using precomputed tables to convert stolen password hashes into plaintext passwords.

- Q6. Why is Password Spraying dangerous?
A:
Low and slow
Avoids lockout
Harder to detect

# ⚡ Active Recall Flashcards
- Q:
Many passwords against one account?
A:
Brute Force
- Q:
One password against many accounts?
A:
Password Spraying
- Q:
Common password list attack?
A:
Dictionary Attack
- Q:
Dictionary + customized variations?
A:
Hybrid Attack
- Q:
Uses leaked credentials?
A:
Credential Stuffing
- Q:
Uses stolen password hashes?
A:
Rainbow Table Attack
- Q:
Floods user with MFA requests?
A:
MFA Fatigue Attack
- Q:
Windows Event ID for failed login?
A:
4625
- Q:
Windows Event ID for successful login?
A:
4624
- Q:
Windows Event ID for NTLM authentication?
A:
4776
- Q:
Windows Event ID for account lockout?
A:
4740

# 🔥 Must Remember
Common Targets
- RDP (3389)
- SSH (22)
- VPN Portals
- Web Applications
- Database Login Panels

# SOC Investigation Workflow
When alert says:
- Multiple Failed Logins

Check:
- Source IP
- Geo Location
- Username targeted
- Time frequency
- Account lockout?
- Any successful login after failures?

⚠️ Successful login after many failures = Escalate immediately

# Important Logs
Windows
- 4625 = Failed Login
- 4624 = Successful Login
- 4776 = NTLM Authentication
- 4740 = Account Lockout

Linux
- /var/log/auth.log

Firewall
- Repeated connection attempts
- Blocked connection spikes

Prevention
- MFA
- Account Lockout
- Rate Limiting
- CAPTCHA
- Geo-Blocking
- Strong Password Policy
- Disable Default Accounts

# 🧠 SOC Analyst Mindset
When you see:
- Multiple Failed Logins

Don't ask:
- "Is this just a login failure?"

Ask:
Is it Brute Force?
Password Spraying?
Credential Stuffing?
Did any login succeed after failures?

Because:
- Failed Login + Successful Login = Possible Compromise

# comparison table
| Attack | Key idea |
|--------|----------|
|Brute force |many passwords -> one user |
|Reverse brute force |one password -> many user |
|Dictionary |common password list |
|Password spraying |one password -> many accounts |
|Hybrid |dictionary + variations |
|Rainbow table |crack hashes offline |
|Credential stuffing |reuse leaked credentials |
|MFA fatigue |spam MFA Prompts until approved |
