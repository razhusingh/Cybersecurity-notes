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
 Q1. What is Brute Force Attack?

- A: Trying all possible password combinations until one works.

 Q2. Difference between Brute Force and Password Spraying?
  
- A: Brute Force
Many passwords → One user
Password Spraying
One password → Many users

 Q3. What is Credential Stuffing?
  
- A: Using leaked username/password combinations from previous breaches.

 Q4. What is MFA Fatigue?
  
- A: Repeated MFA requests sent to victim until they approve login.

 Q5. What is Rainbow Table Attack?
  
- A: Using precomputed tables to convert stolen password hashes into plaintext passwords.

 Q6. Why is Password Spraying dangerous?
  
- A:
Low and slow
Avoids lockout
Harder to detect

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

Based on SOC Analyst L1 Day 8 – Password Attacks.

# Question Paper Mode
1. What is a Brute Force Attack?

2. How does a Brute Force Attack work?

3. What are the SOC indicators of a Brute Force Attack?

4. Name some common Brute Force tools.

5. What is a Reverse Brute Force Attack?

6. What is a Dictionary Attack?

7. What are the SOC indicators of a Dictionary Attack?

8. What is Password Spraying?

9. Why is Password Spraying effective?

10. What are the SOC indicators of Password Spraying?

11. What is a Hybrid Attack?

12. What is a Rainbow Table Attack?

13. what is Credential Stuffing?

14. What are the SOC indicators of Credential Stuffing?

15. What is an MFA Fatigue Attack?

16. What are the SOC indicators of an MFA Fatigue Attack?

17. Which services are commonly targeted by password attacks?

18. What should a SOC Analyst investigate after multiple failed login alerts?

19. Which Windows Event IDs should every SOC Analyst remember?

20. Which Linux log file records SSH login attempts?

21. Name common password attack prevention mechanisms.

22. Which password attack is easiest to detect?

23. Which password attacks are most difficult to detect?

24. Which password attack is performed offline?

25. Explain the ransomware attack chain involving password attacks. 

26. What is the difference between Brute Force Attack and Password Spraying?

27. Which password attack uses previously leaked credentials?

28. Which password attack repeatedly sends MFA push notifications?

29. Which password attack uses precomputed hash tables?

30. Which password attack is considered an offline attack?

31. Which password attack is most common in ransomware incidents?

32. Which password attack is the easiest for SOC teams to detect?

33. Which password attack is the hardest for SOC teams to detect?

34. Which Windows Event ID indicates a failed login?

35. Which Windows Event ID indicates a successful login?

36. Which Windows Event ID is related to NTLM authentication?

37. Which Windows Event ID indicates an account lockout?

38. During a brute force attack, which log should a SOC analyst check first?

39. Why is account lockout policy important?

40. Why is MFA an effective defense against password attacks?

# Answer Key

1. An attacker tries every possible password combination until the correct password is found.

2. The attacker sends thousands of login attempts until one succeeds, especially if no account lockout policy exists.

3.
```
Event ID 4625 (Failed Login)
Multiple attempts from same IP
Same username targeted repeatedly
High authentication failures
Frequent login attempts
```
5.
```
Hydra
Burp Suite
Medusa
Ncrack
```
5. One common password is tried against many user accounts.

6. An attacker uses a wordlist of common passwords instead of trying every possible combination.

7.
```
Common password patterns
Moderate-speed login attempts
Attempts across multiple systems
```
8. One password is tried against many user accounts.

9. It avoids account lockout and exploits predictable passwords.

10.
```
One password across many usernames
Attempts spread over time
No account lockout
Multiple usernames targeted
```
11. A combination of dictionary words with customized password variations.

12. An attack that uses precomputed hash tables to recover plaintext passwords from stolen hashes.

13. Using leaked username-password combinations from previous breaches to access other services.

14.
```
Login attempts from multiple IPs
Valid credentials from unusual locations
Impossible travel alerts
High login success after previous failures
```
15. Repeated MFA prompts are sent until the victim accidentally approves one.

16.
```
Multiple MFA requests
Successful login after repeated MFA prompts
```
17.
```
RDP (3389)
SSH (22)
VPN Portals
Web Applications
Database Login Panels
```
18.
```
Source IP
Geo Location
Username
Success or Failure
Login Frequency
Account Lockout
Successful login after failures
```
19.
```
4625 → Failed Login
4624 → Successful Login
4776 → NTLM Authentication
4740 → Account Lockout
```
20. /var/log/auth.log

21.
```
Account Lockout Policy
MFA
Rate Limiting
CAPTCHA
Geo-blocking
Strong Password Policy
Disable Default Accounts
```
22. Brute Force Attack.

23. Password Spraying, Credential Stuffing and MFA Fatigue Attack.

24. Rainbow Table Attack.

25. Phishing → Credential Theft → VPN Login Attempt → MFA Failure → Password Spraying → Weak Service Account Compromised → Internal Access.

26.
```
Brute Force: Many passwords → One user.
Password Spraying: One password → Many users.
```
27. Credential Stuffing.

28. MFA Fatigue Attack.

29. Rainbow Table Attack.

30. Rainbow Table Attack.

31. Password Spraying and Credential Stuffing are commonly seen in ransomware attack chains.

32. Brute Force Attack.

33. Password Spraying, Credential Stuffing, and MFA Fatigue Attack.

34. Event ID 4625 (Failed Login).

35. Event ID 4624 (Successful Login).

36. Event ID 4776 (NTLM Authentication).

37. Event ID 4740 (Account Lockout).

38.
Check:
```
Source IP
Username
Login frequency
Success/Failure
Geo-location
Account lockout status
```
40. It blocks repeated login attempts after multiple failures, reducing the risk of brute force attacks.

41. Even if an attacker knows the correct password, they still need the second authentication factor to access the account.
