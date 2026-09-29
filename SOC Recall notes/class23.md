# SOC Analyst L1 — Class 23
# Linux File System, Permissions, Logs & SSH

---

# 1. ⚡ 30-SECOND RECALL

## Linux File System

    /        → Root
    /bin     → User binaries
    /sbin    → System binaries
    /etc     → Configuration
    /dev     → Devices
    /home    → User home
    /usr     → User programs/libraries
    /tmp     → Temporary files
    /var     → Variable data / logs
    /boot    → Boot files/kernel
    /root    → Root user's home
    /lib     → Libraries
    /opt     → Optional software
    /mnt     → Mount point
    /media   → Removable media
    /srv     → Service data
    /sys     → Kernel information
    /proc    → Process/system information

---

# 2. 🔥 MUST REMEMBER — LINUX PERMISSIONS

Three permissions:

    r = Read
    w = Write
    x = Execute

Numeric values:

    r = 4
    w = 2
    x = 1

Common:

    7 = rwx
    6 = rw-
    5 = r-x
    4 = r--
    0 = ---

Permission groups:

    u = User/Owner
    g = Group
    o = Others

Example:

    -rwxr-xr--

    User   → rwx
    Group  → r-x
    Others → r--

---

# 3. 🔥 PERMISSION MEANING

## File

    r → Read contents
    w → Modify contents
    x → Execute file

## Directory

    r → List contents
    w → Create/Delete/Rename
    x → Enter directory

### Important

To delete a file:

    Write + Execute
    on parent directory

---

# 4. 🔥 CHMOD

Example:

    chmod 644 file.txt

Means:

    Owner  → rw-
    Group  → r--
    Others → r--

Remember:

    644 = rw-r--r--

---

# 5. 🔥 LINUX LOGS

Main directory:

    /var/log/

Important:

    /var/log/auth.log
    → Authentication
    → SSH logins
    → Failed logins
    → sudo

    /var/log/syslog
    → General system logs

    /var/log/kern.log
    → Kernel logs

    /var/log/secure
    → Authentication
    → RHEL/CentOS

    /var/log/messages
    → General system activity

    /var/log/apache2/access.log
    → Web access

    /var/log/apache2/error.log
    → Web server errors

### 🔥 MUST REMEMBER

    auth.log / secure
          ↓
    Authentication Investigation

---

# 6. 🔥 AUTHENTICATION LOG

Example:

    Accepted password for admin
    from 192.168.1.10

Can reveal:

    Date
    Time
    Host
    User
    Authentication result
    Source IP

---

# 7. 🔥 SSH

SSH = Secure Shell

Purpose:

    Remote Linux Access

Default port:

    22

Components:

    ssh  → Client
    sshd → Server/Daemon

Attackers may abuse SSH for:

- Remote control
- Persistence
- Lateral movement

---

# 8. SSH AUTHENTICATION

Two methods:

    1. Password Authentication
    2. Key-Based Authentication

## Password

    Username + Password
          ↓
    Encrypted SSH Tunnel
          ↓
    Server
          ↓
    /etc/shadow

Risk:

    Brute Force

---

# 9. 🔥 KEY-BASED AUTHENTICATION

Uses:

    Public Key
    +
    Private Key

Examples:

    RSA
    Ed25519

Location:

    Private Key → Client

    Public Key → Server

Public key stored in:

    ~/.ssh/authorized_keys

### Remember

    Private Key → Keep on Client
    Public Key  → Server

---

# 10. SSH KEY AUTHENTICATION FLOW

    Client
      ↓
    Selects Key
      ↓
    Server Sends Challenge
      ↓
    Public Key Encryption
      ↓
    Client Uses Private Key
      ↓
    Signature Sent
      ↓
    Server Verifies
      ↓
    Authentication Successful

---

# 11. SSH CONFIGURATION

SSH server configuration:

    /etc/ssh/sshd_config

---

# 12. 🔥 SSH PERSISTENCE

Attack scenario:

    Attacker gains access
          ↓
    Adds SSH Public Key
          ↓
    ~/.ssh/authorized_keys
          ↓
    Future SSH Access
          ↓
    Persistence

---

# 13. 🔥 REAL SOC SCENARIO

    Many Failed SSH Logins
             ↓
       Successful Login
             ↓
         sudo Activity
             ↓
         Brute Force
             ↓
         Compromise
             ↓
    Privilege Escalation

---

# 14. 🧠 SOC ANALYST MINDSET

When investigating Linux login activity, ask:

    WHO?
    ↓
    Who logged in?

    FROM WHERE?
    ↓
    What was the source IP?

    HOW?
    ↓
    Password or SSH Key?

    WHAT NEXT?
    ↓
    What happened after login?

    PRIVILEGE?
    ↓
    Was sudo used?

---

# 15. ⭐ INTERVIEW Q&A

### Q1. What is the Linux root directory?

`/` is the root of the Linux file system hierarchy.

### Q2. What is `/etc`?

Contains system configuration files.

### Q3. What is `/var/log`?

Main directory containing Linux log files.

### Q4. What is `/var/log/auth.log`?

Authentication-related log, commonly used on Debian/Ubuntu systems.

### Q5. What is `/var/log/secure`?

Authentication-related log commonly used on RHEL/CentOS systems.

### Q6. What does `rwx` mean?

    r = Read
    w = Write
    x = Execute

### Q7. What are the numeric values?

    r = 4
    w = 2
    x = 1

### Q8. What does 644 mean?

    Owner  → rw-
    Group  → r--
    Others → r--

### Q9. What is SSH?

Secure Shell, used for remote Linux access.

### Q10. What is the default SSH port?

    22

### Q11. What is the difference between ssh and sshd?

    ssh  → Client
    sshd → Server/Daemon

### Q12. Where is the SSH public key stored?

    ~/.ssh/authorized_keys

### Q13. Where is SSH server configuration stored?

    /etc/ssh/sshd_config

### Q14. Why is SSH important for SOC?

Because attackers can abuse SSH for remote control, persistence and lateral movement.

---

# 16. 📝 QUESTION PAPER MODE

1. What is the Linux root directory?
2. What is `/bin`?
3. What is `/etc`?
4. What is `/var`?
5. What is `/proc`?
6. What is `/sys`?
7. What are Linux file permissions?
8. What do r, w and x mean?
9. What are the numeric values of r, w and x?
10. What do u, g and o mean?
11. What does `644` mean?
12. What permissions are needed to delete a file?
13. What is `/var/log`?
14. What is `/var/log/auth.log`?
15. What is `/var/log/secure`?
16. What is `/var/log/syslog`?
17. What is SSH?
18. What is the default SSH port?
19. What is ssh?
20. What is sshd?
21. What are the two SSH authentication methods?
22. What is key-based authentication?
23. Where is the SSH public key stored?
24. What is `/etc/ssh/sshd_config`?
25. How can attackers use SSH for persistence?
26. What does many failed SSH logins followed by a successful login and sudo activity indicate?
27. What should a SOC analyst check after a suspicious Linux login?

---

# 17. ✅ ANSWER KEY

1. `/`
2. User binary executables.
3. Configuration files.
4. Variable data including logs.
5. Virtual file system containing process/system information.
6. Kernel-related information.
7. Rules controlling access to files/directories.
8. Read, Write, Execute.
9. r=4, w=2, x=1.
10. User/Owner, Group, Others.
11. Owner rw-, Group r--, Others r--.
12. Write + Execute on the parent directory.
13. Main Linux log directory.
14. Authentication logs, including SSH and sudo activity.
15. Authentication logs on RHEL/CentOS.
16. General system logs.
17. Secure Shell for remote Linux access.
18. 22.
19. SSH client.
20. SSH server/daemon.
21. Password and key-based authentication.
22. Authentication using public/private key pairs.
23. `~/.ssh/authorized_keys`.
24. SSH server configuration file.
25. By adding an attacker's public key to `authorized_keys`.
26. Possible brute-force compromise followed by privilege escalation.
27. Who logged in, source IP, authentication method, subsequent activity and privilege escalation/sudo activity.

---

# 🔥 FINAL L1 MEMORY MAP

    LINUX
      ↓
    File System
      ↓
    Permissions
      ↓
    /var/log
      ↓
    Authentication Logs
      ↓
    SSH
      ↓
    Port 22
      ↓
    Login
      ↓
    What happened next?
      ↓
    sudo / Privilege Escalation
      ↓
    Attack Story

### Core Memory

    r = 4
    w = 2
    x = 1

    644 = rw-r--r--

    SSH = 22

    ssh  = Client
    sshd = Server

    auth.log / secure
    = Authentication Logs

    authorized_keys
    = SSH Public Keys