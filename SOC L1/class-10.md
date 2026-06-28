# Lateral movement and Privilege Escalation

# Lateral movement
lateral movement is when an attacker moves from one compromised system to other systems inside a network.

Instead of leaving the network, the attacker moves sideways across machines

Attackers do this to:
- find valuable data
- reach domain controllers
- access admin accounts
- deploy ransomware across the network

# Typical attack path
phishing -> user laptop compromise -> lateral movement -> domain controller -> full network control

# why attackers perform lateral movement
Because the first compromised system rarely has valuable data

example:
- attacker compromises:
- Employee laptop

but target is:
- file server
- domain controller
- database server

so attacker moves across the network

# common lateral movement techniques
1. Pass-the-hash(pth)
- Attacker steals password hashes from memory

instead of cracking password, they reuse the hash directly

example tools:
- mimikatz
- crackmapexec

soc indicators:
- NTLM authentication anomalies
- logins without password usage

2. Pass-the-Ticket(kerberos attack)
- Attacker steals kerberos authentication tickets

then uses them to access other machines

soc indicators:
- suspicious kerberos ticket usage
- unusual TGT activity

3. remote desktop protocol(RDP)
- attacker uses stolen credentials to connect via:
port 3389

Soc indicators:
- internal RDP connections
- unusaual login locations
- login outside working hours

4. SMB / windows admin shares
- attacker copies tools across machines using:
\\\target\c$

common tools:
- psExec
- impacket
- crackMapExec

soc indicators:
- admin share access
- suspicious file transfers
- service creation events

5. Windows management instrumentation(WMI)
- Allo;ws remote command execution

example command:
- wmic /node:target process call create "malware.exe"

soc indicators:
- WMI process creation
- remote execution logs

# Real soc scenario
Alert sequence:
- suspicious login to user laptop
- Mimikatz executed
- admin credentials dumped
- attacker logs into file server
- ransomware deployed

step 4 is lateral movement

# Privilege escalation
Privilege escalaton is when an attacker gains higher permissions than originally allowed

example:
- user account -> adminsitrator access

- step 0 = pre-engagement
- step 1 = passive recon 
- step 2 = active recon
- step 3 = service enumeration
- step 4 = access eexploitation 
- step 5 = privilege escalation

# privilege escalation - two types
1. vertical privilege escalation

user -> admin

example:
- normal user -> local admin -> domain admin

2. Horizontal privilege escalation

user -> another user

example:
- employee account -> manager account
same level but different privileges

# why attacker need privilege escaltion
because initial compromise often gives:
- low privilege access but attackers want:
Administrator / root / domain admin

which allows them to:
- disable security tools
- dump credentials
- access servers
- deploy ransomware

# comon privilege escalation techniques
1. exploiting software vulnerabilities

example:
- outdated windows kernel
- vulnerable drivers

attacker runs exploit -> becomes admin

2. Credential dumping
tools like:
- mimikatz
- LSASS memory dumping

extract admin passwords

soc indicators:
- LSASS process access
- credential dumping alerts

3. Misconfigured permissions
example:
- service runs as system but executable is writable

- attacker replaces file -> gains admin access

4. token impersonation
- windows access token stolen from high-privilege processes

attacker impersonates admin

5. cheduled task abuse
attacker modifies scheduled tasks running as admin

Watch for:
- sudden admin rights assignment
- new admin account creation
- service creation events
- suspicious LSASS access
- privilege escalation exploits

# Important windows event ids:
|Event ID |Meaning |
|---------|--------|
|4672 |special privileges assigned |
|4688 |process creation |
|4720 |user account created |
|4732 |user added to admin group |

# Attack chain
Real ransomware scenario:
```
phishing email
|
user laptop compromise
|
credential dumping
|
privilege escalation
|
lateral movement
|
domain controller access
|
ransomware deployment
```

# Difference between lateral movement and privilege escalation
| feature |lateral movement |privilege escalation |
|---------|-----------------|---------------------|
|goal |move across systems |gain higher permissions |
|direction |sideways |upwards |
|example |laptop -> server |user -> admin |
|purpose |expand access |gain control |



