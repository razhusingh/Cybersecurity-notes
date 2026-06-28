 Day 10 (Lateral Movement & Privilege Escalation)

# 30-Second Recall
- Lateral Movement = Sideways movement across compromised systems.

- Privilege Escalation = Gaining higher permissions.

- Initial compromise rarely has valuable data.

- Goal = Domain Controller, Admin Accounts, File Servers.

- Pass-the-Hash (PtH) = Reuse NTLM hash.

- Pass-the-Ticket (PtT) = Reuse Kerberos ticket.

- RDP = Port 3389.

- SMB Admin Share = \\target\C$.

- WMI = Remote command execution.

- Vertical Privilege Escalation = User → Admin.

- Horizontal Privilege Escalation = User → Another User.

- Credential Dumping = Mimikatz + LSASS.

- Event ID 4672 = Special privileges assigned.

- Event ID 4688 = Process creation.

- Event ID 4720 = User account created.

- Event ID 4732 = User added to Admin group.

- Attack Chain = Phishing → Credential Dumping → Privilege Escalation → Lateral Movement → Domain Controller → Ransomware.

-Lateral Movement = Sideways.

-Privilege Escalation = Upwards.

# Must Remember

- ✅ Lateral Movement = Sideways movement

- ✅ Privilege Escalation = Higher permissions

- ✅ PtH = NTLM Hash reuse

- ✅ PtT = Kerberos Ticket reuse

- ✅ RDP = Port 3389

- ✅ SMB Admin Share = \\target\C$

- ✅ WMI allows remote execution

- ✅ Vertical = User → Admin

- ✅ Horizontal = User → Another User

- ✅ Mimikatz + LSASS = Credential Dumping

- ✅ Attack Chain:

Phishing → Credential Dumping → Privilege Escalation → Lateral Movement → Domain Controller → Ransomware

# Interview Q&A
- What is Lateral Movement?

Attacker moves from one compromised machine to other systems inside the network.

- Why do attackers perform Lateral Movement?

To reach valuable assets like file servers, admin accounts and domain controllers.

- What is Pass-the-Hash?

Using stolen NTLM password hashes without knowing the password.

- What is Pass-the-Ticket?

Using stolen Kerberos tickets to authenticate.

- Which port does RDP use?

3389

- What is SMB Admin Share?

Windows administrative share (\\target\C$) used to copy files remotely.

- What is WMI?

Windows Management Instrumentation used for remote command execution.

- What is Privilege Escalation?

Obtaining higher permissions than originally assigned.

- Difference between Vertical & Horizontal Privilege Escalation?
Vertical → User to Admin.
Horizontal → User to another user at same privilege level.

- Why do attackers need Privilege Escalation?

To disable security tools, dump credentials, access servers and deploy ransomware.

Name common Privilege Escalation techniques.
- Software Vulnerabilities
- Credential Dumping
- Misconfigured Permissions
- Token Impersonation
- Scheduled Task Abuse

Important Windows Event IDs?
- 4672, 4688, 4720, 4732.

- Difference between Lateral Movement & Privilege Escalation?
Lateral = Sideways movement across systems.
Privilege Escalation = Higher permissions.

# SOC Analyst Mindset
 Lateral Movement Indicators
- Internal RDP connections
- NTLM authentication anomalies
- Suspicious Kerberos ticket usage
- Admin share access
- WMI remote execution
- Service creation events
- Login outside business hours

Privilege Escalation Indicators
- Sudden admin rights
- New admin account
- LSASS access
- Credential dumping alerts
- Privilege escalation exploits
- User added to Admin group

# SOC Attack Flow
```
Phishing

↓

Laptop Compromise

↓

Credential Dumping

↓

Privilege Escalation

↓

Lateral Movement

↓

Domain Controller

↓

Ransomware
```

# Question Paper Mode
- What is Lateral Movement?

- Why do attackers perform Lateral Movement?

- What is Pass-the-Hash?

- What is Pass-the-Ticket?

- Which port does RDP use?

- What is SMB Admin Share?

- What is WMI?

- What is Privilege Escalation?

- Difference between Vertical and Horizontal Privilege Escalation?

- Why do attackers need Privilege Escalation?

- Name five Privilege Escalation techniques.

- What are common indicators of Lateral Movement?

- What are common indicators of Privilege Escalation?

- What does Windows Event ID 4672 represent?

- What does Event ID 4688 represent?

- What does Event ID 4720 represent?

- What does Event ID 4732 represent?

- Explain the ransomware attack chain.

- Difference between Lateral Movement and Privilege Escalation.

- In the sequence Mimikatz → LSASS Access → Admin Login → RDP to File Server, identify each attack stage.

# Answer Key
1. Moving sideways across compromised systems.

2. To reach valuable assets such as file servers, admin accounts and domain controllers.

3. Reusing stolen NTLM password hashes.

4. Reusing stolen Kerberos authentication tickets.

5. Port 3389.

6. Windows administrative share (\\target\C$) used for remote administration.

7. Windows Management Instrumentation for remote command execution.

8. Gaining higher permissions than originally assigned.

9. Vertical = User → Admin; Horizontal = User → Another User.

10. To disable security tools, dump credentials, access sensitive systems and deploy ransomware.

11. Software Vulnerabilities, Credential Dumping, Misconfigured Permissions, Token Impersonation, Scheduled Task Abuse.

12. NTLM anomalies, Kerberos anomalies, internal RDP, SMB admin share access, WMI execution, service creation.

13. Admin rights assignment, LSASS access, new admin accounts, privilege escalation exploits, service creation.

14. Special privileges assigned.

15. Process creation.

16. User account created.

17. User added to Administrator group.

18. Phishing → Credential Dumping → Privilege Escalation → Lateral Movement → Domain Controller → Ransomware.

19. Lateral Movement = Sideways movement across systems. Privilege Escalation = Upward movement to gain higher permissions.

```
Mimikatz → Credential Dumping
LSASS Access → Credential Dumping
Admin Login → Privilege Escalation
RDP to File Server → Lateral Movement

```
