# SOC Analyst L1 — Class 23
# Linux File System, Permissions, Logs & SSH
---

# 1. Linux File System Structure

## What is Linux File System?

Linux organizes everything in a single **hierarchical tree structure**.

Unlike Windows, which commonly uses:

    C:\
    D:\
    E:\

Linux starts from:

    /

This is called the:

    ROOT DIRECTORY

Everything in the Linux file system starts from `/`.

---

# 2. Linux File System Structure

The main directories shown in the PDF are:

| Directory | Purpose |
|---|---|
| `/` | Root directory |
| `/bin` | User binary executables |
| `/sbin` | System binary executables |
| `/etc` | Configuration files |
| `/dev` | Device files representing hardware devices |
| `/home` | Home directories for users |
| `/usr` | User programs and libraries |
| `/tmp` | Temporary files |
| `/var` | Variable data such as logs/database files |
| `/boot` | Boot loader files and kernel images |
| `/root` | Home directory of the root user |
| `/lib` | System libraries |
| `/opt` | Optional/add-on application software packages |
| `/mnt` | Mount point for file systems |
| `/media` | Removable media |
| `/srv` | Service data |
| `/sys` | Kernel-related information |
| `/proc` | Virtual file system containing system/process information |

---

# 3. Important Linux Directories

## `/bin`

Contains essential user command binaries.

Examples shown in the diagram include:

    bash
    cat
    chmod
    cp
    date
    echo
    grep
    gzip
    hostname
    kill
    ls
    mkdir
    more
    mount
    mv
    ping
    ps
    pwd
    rm
    sh
    su
    tar
    touch
    umount
    uname

---

## `/sbin`

Contains essential system binaries.

Examples shown include:

    fdisk
    fsck
    getty
    halt
    ifconfig
    init
    mkfs
    mkswap
    reboot
    route

---

## `/etc`

Contains configuration files for the system.

Examples shown include:

    crontab
    cups
    fstab
    hosts
    hostname
    hosts.allow
    hosts.deny
    init.d
    issue
    machine-id
    mtools.conf
    nanorc
    networks
    passwd
    profile
    protocols
    resolv.conf
    rpc
    securetty
    services
    shells
    timezone

---

## `/usr`

Contains user applications, programs and libraries.

Important subdirectories shown:

    /usr/bin
    /usr/include
    /usr/lib
    /usr/local
    /usr/share

### `/usr/bin`

Contains many commonly used user commands.

### `/usr/include`

Contains standard include files for C code.

### `/usr/lib`

Contains libraries such as:

    .o
    .bin
    .lib

for coding and packages.

### `/usr/local`

Contains locally installed software.

Subdirectories shown:

    /usr/local/bin
    /usr/local/lib
    /usr/local/man
    /usr/local/sbin
    /usr/local/share

### `/usr/share`

Contains static/shareable data.

Example:

    /usr/share/man

contains manual pages.

---

# 4. `/var`

`/var` contains variable data files.

Examples shown:

    /var/cache
    /var/lib
    /var/lock
    /var/log
    /var/opt
    /var/spool
    /var/tmp

## Important

### `/var/cache`

Application cache data.

### `/var/lib`

Data modified as programs run.

### `/var/lock`

Lock files used to track resources currently in use.

### `/var/log`

Log files.

### `/var/opt`

Variable data for installed packages.

### `/var/spool`

Tasks waiting to be processed.

Examples:

    /var/spool/cups
    /var/spool/mail

### `/var/tmp`

Temporary files saved between reboots.

---

# 5. Other Important Directories

## `/dev`

Contains device files representing hardware devices.

Example shown:

    /dev/null

---

## `/home`

Contains user home directories.

Example:

    /home/user

---

## `/mnt`

Mount point for temporary file systems.

---

## `/media`

Used for removable media.

---

## `/proc`

A virtual file system containing information about:

- Processes
- System
- Network status
- Other system information

---

## `/sys`

Contains kernel-related information.

The PDF describes it as similar to `/proc`, but with more detailed kernel-related information.

---

## `/root`

Home directory of the root user.

---

## `/boot`

Contains:

- Boot loader files
- Kernel images

---

## `/lib`

Contains system libraries.

---

## `/opt`

Contains optional/add-on application software packages.

---

## `/srv`

Contains service data.

---

# 6. Linux Permissions

In Linux:

> Everything is treated as a file.

Every file has:

- An owner
- A group

Permissions define how:

- Owner
- Group
- Everyone else

can interact with the file.

The three basic permissions are:

    Read
    Write
    Execute

---

# 7. Read Permission — `r`

Symbol:

    r

## For a File

Read permission means:

    View the file contents

## For a Directory

Read permission means:

    List the files inside

Example:

    ls

---

# 8. Write Permission — `w`

Symbol:

    w

## For a File

Write permission means:

    Modify the file contents

## For a Directory

Write permission allows:

- Create files
- Delete files
- Rename files

inside the directory.

---

# 9. Execute Permission — `x`

Symbol:

    x

## For a File

Execute permission means:

    Run the file as a program

## For a Directory

Execute permission means:

    Enter the directory

Example:

    cd

---

# 10. Important File Deletion Point

To delete a file, you need:

    Write + Execute

permissions on the **parent directory**.

You do not necessarily need write permission on the file itself.

Example:

    /home/user/
          |
          └── file.txt

To delete `file.txt`, the relevant permissions are on:

    /home/user/

---

# 11. Linux Permission Structure

Command:

    ls -l

may show:

    -rwxr-xr--

The first character represents the file type.

## First Character

    -
    → Regular file

    d
    → Directory

    l
    → Symbolic link

---

# 12. Permission Triplets

After the file-type character, the next nine characters are divided into three groups.

    -rwxr-xr--
     ||| ||| |||
     ||| ||| |||
     u   g   o

Where:

    u = User / Owner
    g = Group
    o = Others

---

# 13. Example — `-rwxr-xr--`

Given:

    -rwxr-xr--

## User / Owner

    rwx

Meaning:

- Read
- Write
- Execute

## Group

    r-x

Meaning:

- Read
- No Write
- Execute

## Others

    r--

Meaning:

- Read
- No Write
- No Execute

---

# 14. Numeric / Octal Permission Notation

Linux permissions can also be represented using numbers.

Values:

    Read    = 4
    Write   = 2
    Execute = 1
    None    = 0

---

# 15. Calculating Permission Values

For one permission triplet, add the values.

Example:

    r + w + x

    4 + 2 + 1 = 7

Therefore:

    rwx = 7

---

# 16. Common Numeric Permissions

| Number | Permission | Meaning |
|---|---|---|
| `7` | `rwx` | Full control |
| `6` | `rw-` | Read and write |
| `5` | `r-x` | Read and execute |
| `4` | `r--` | Read-only |
| `0` | `---` | No access |

---

# 17. `chmod`

The PDF gives:

    chmod 644 file.txt

This sets:

    Owner  → rw-
    Group  → r--
    Others → r--

Therefore:

    644
     ↓
    Owner  = Read + Write
    Group  = Read-only
    Others = Read-only

---

# 18. Linux `/var/log`

## What is `/var/log`?

`/var/log` is the main Linux logging directory.

It contains:

- Authentication logs
- System logs
- Application logs

## Why SOC Cares

Linux investigation heavily depends on:

    Log Analysis

SOC analysts use logs to understand activity on Linux systems.

---

# 19. Important `/var/log` Files

## `/var/log/auth.log` 🔥

The PDF marks this as:

    MOST IMPORTANT

It contains information such as:

- SSH logins
- Authentication attempts
- `sudo` usage

---

# 20. `/var/log/syslog`

Contains:

    General system logs

---

# 21. `/var/log/kern.log`

Contains:

    Kernel logs

---

# 22. `/var/log/secure`

Used in:

- Red Hat
- CentOS

It is the authentication-log equivalent used on these systems.

---

# 23. `/var/log/messages`

Contains:

    General system activity

---

# 24. Apache Logs

## `/var/log/apache2/access.log`

Contains:

    Web access logs

## `/var/log/apache2/error.log`

Contains:

    Web server errors

---

# 25. Linux Authentication Logs

Authentication logs track:

- User logins
- SSH access
- Failed logins
- `sudo` usage

## Main Files

| OS | Authentication Log |
|---|---|
| Ubuntu/Debian | `/var/log/auth.log` |
| RHEL/CentOS | `/var/log/secure` |

---

# 26. Authentication Log Example

Example shown in the PDF:

    Jul 10 10:22:11 server sshd[2345]:
    Accepted password for admin from 192.168.1.10

Important information visible:

- Date
- Time
- Host
- SSH daemon
- User
- Authentication result
- Source IP

Example interpretation:

    admin
      ↓
    Successful SSH password authentication
      ↓
    Source IP = 192.168.1.10

---

# 27. SSH — Secure Shell

SSH stands for:

    Secure Shell

It provides:

    Remote Linux Access

Default port:

    22

---

# 28. Why Attackers Love SSH

The PDF lists:

- Remote control
- Persistence
- Lateral movement

SSH can therefore be important during Linux security investigations.

---

# 29. SSH Components

## `ssh`

Client command.

Used from the client side to initiate SSH connections.

Example:

    ssh username@host

---

## `sshd`

SSH daemon.

It is the:

    SSH server process

---

## Port

Default SSH port:

    22

---

# 30. SSH Authentication Methods

The PDF covers two main methods:

1. Password Authentication
2. Key-Based Authentication

---

# 31. Password Authentication

Password authentication uses:

    Username + Password

The client sends the username and password through the encrypted SSH tunnel.

The server checks the credentials against:

    /etc/shadow

on Linux.

## Advantage

Simple to use.

## Weakness

It can be vulnerable to:

    Brute-Force Attacks

---

# 32. Key-Based Authentication

Key-based authentication is described as:

    More Secure

It uses:

- Public Key
- Private Key

It uses asymmetric encryption.

The PDF mentions:

    RSA
    Ed25519

as examples.

The PDF describes this as the most common professional method.

---

# 33. Public Key and Private Key

## Private Key

- Kept on the user's machine
- Must remain protected

## Public Key

Placed on the server in:

    ~/.ssh/authorized_keys

Basic relationship:

    Private Key → Client
    Public Key  → Server

---

# 34. SSH Key Authentication — Challenge Process

The PDF's authentication flow is:

### Step 1

Client tells the server which key it wants to use.

### Step 2

Server generates a random number called a:

    Challenge

The server encrypts the challenge using the user's:

    Public Key

and sends it to the client.

### Step 3

Only the corresponding:

    Private Key

can decrypt the message.

The client:

- Decrypts the message
- Combines it with the session ID
- Sends a signature back

### Step 4

The server verifies the signature.

If the signature matches:

    Authentication Successful

---

# 35. SSH Diagram Flow

    SSH Client
         ↓
    Username + Host
         ↓
    Username / Host / Private Key
         ↓
    Message sent as packets
         ↓
    SSH Server
         ↓
    Private Key verified
         ↓
    Matching key in:
    ~/.ssh/authorized_keys
         ↓
    User Authentication Layer
         ↓
    Authentication successful

The diagram also shows that the user-authentication layer can be used to:

- Run commands on the SSH server terminal
- Send files
- Receive files
- Initiate tunneling between the two servers

---

# 36. SSH Configuration

SSH server configuration file:

    /etc/ssh/sshd_config

This is the SSH configuration file shown in the PDF.

---

# 37. SSH SOC Importance

Attackers may add their own SSH keys for:

    Persistence

Example concept:

    Attacker gains access
          ↓
    Adds SSH public key
          ↓
    Key remains authorized
          ↓
    Future SSH access
          ↓
    Persistence

---

# 38. Real SOC Investigation Scenario

The PDF provides this scenario:

    Many Failed SSH Logins
            ↓
        Then Success
            ↓
        Then sudo Activity

SOC interpretation:

    Brute Force
         ↓
    Compromise
         ↓
    Privilege Escalation

---

# 39. SOC Investigation Flow

When investigating suspicious SSH activity:

    Failed SSH Logins
           ↓
    Successful SSH Login
           ↓
    sudo Activity
           ↓
    Investigate Privilege Escalation

The sequence is important.

A large number of failed logins followed by a successful login can indicate possible account compromise.

---

# 40. Final Linux SOC Mindset

When investigating Linux activity, do not ask only:

    "Was there a login?"

Ask:

    Who logged in?
          ↓
    From where?
          ↓
    Using what method?
          ↓
    What happened after login?
          ↓
    Was privilege escalation used?

---

# 41. Linux Investigation Mindset

## WHO?

Identify the account that logged in.

## FROM WHERE?

Identify the source IP/location shown by the logs.

## USING WHAT METHOD?

Determine whether authentication used:

- Password
- SSH key

## WHAT HAPPENED AFTER LOGIN?

Look at subsequent activity.

## PRIVILEGE ESCALATION?

Check whether:

    sudo

or other privileged activity occurred.

---

# 42. Linux SOC Quick Reference

## File System

    /     → Root
    /bin  → User binaries
    /sbin → System binaries
    /etc  → Configuration
    /dev  → Devices
    /home → User homes
    /usr  → User programs/libraries
    /tmp  → Temporary files
    /var  → Variable data
    /boot → Boot/kernel files
    /root → Root user's home
    /lib  → System libraries
    /opt  → Optional software
    /mnt  → Mount point
    /media → Removable media
    /srv  → Service data
    /sys  → Kernel information
    /proc → Process/system information

---

# 43. Linux Permission Quick Reference

    r = 4
    w = 2
    x = 1

    7 = rwx
    6 = rw-
    5 = r-x
    4 = r--
    0 = ---

Permission groups:

    u = User
    g = Group
    o = Others

Example:

    -rwxr-xr--

    User   → rwx
    Group  → r-x
    Others → r--

---

# 44. Important Linux Logs

    /var/log/
        ↓
    auth.log     → Authentication
    syslog       → General system logs
    kern.log     → Kernel logs
    secure       → Authentication (RHEL/CentOS)
    messages     → General system activity
    apache2/access.log
                 → Web access
    apache2/error.log
                 → Web server errors

---

# 45. SSH Quick Reference

    SSH
      ↓
    Secure Shell
      ↓
    Remote Linux Access
      ↓
    Port 22

Components:

    ssh  → Client
    sshd → Server/Daemon

Authentication:

    Password
       OR
    Public/Private Key

Key authentication:

    Private Key → Client
    Public Key  → ~/.ssh/authorized_keys

SSH configuration:

    /etc/ssh/sshd_config

---

# 46. Real SOC Attack Chain

    Many Failed SSH Logins
            ↓
    Successful SSH Login
            ↓
    sudo Activity
            ↓
    Brute Force
            ↓
    Compromise
            ↓
    Privilege Escalation

---

# 47. Final SOC Investigation Flow

    SSH/Login Event
          ↓
    Who logged in?
          ↓
    From where?
          ↓
    Authentication method?
          ↓
    What happened after login?
          ↓
    sudo / Privilege Activity?
          ↓
    Determine Attack Story

---
