# Malwares

what is malware?
malicious software designed to:
- steal data
- disrupt systems
- gain unauthorized access
- spy on users*
- encrypt files for ransom

# types of malware
- virus
- worm
- trojan
- ransomware
- spyware
- rootkit

1. virus
- a virus attaches itself to a legitimate file and spreads when that file runs

how it works:
- 1. user downloads infected file
- 2. file runs
- 3. virus executes
- 4. spreads to other files

example:
- an infected .exe shared via usb

soc detection:
- unknown process spawning
- suspicious file modification
- antivirus alerts

2. worm
- a worm spreads automatically over networks, no user action needed

key difference:
- virus -> needs user interaction
- worm -> self-propagates

famous example:
- wannacry (spread using smb vulnerability)

soc detectin:
- sudden network traffic spike
- same payload across multiple hosts
- lateral scanning behavior

3. Trojan
- malware disguised as legitimate software

example:
- fake "free cracked software.exe"

what it does:
- open backdoor
- steals data
- installs additional malware

soc detection:
- unusual outbound traffic
- unknown services running
- suspicious startup entries

4. Ransomware
- encrypts victim files and demands ransom payment

- 1. phishing email
- 2. user clicks attachment
- 3. malware installs
- 4. files encrypted
- 5. ransom note displayed

soc indicators:
- mass file renaming
- high cpu usage
- shadow copy deletion
- unusual encryption activity

5. spyware
- secretly collects user information

what it steals:
- passwords
- banking info
- screenshots
- keystrokes (keylogger)

soc detection:
- strange outbound conncetions
- dns queries to unknown domains
- data exfiltration alerts

6. Rootkit
- malware designed to hide other malware

dangerous because:
- hides porcesses
- hides files
- hides registry entries
- very difficult to detect

soc detection:
- mismatch between user-mode and kernel-wode results
- integrity check failures
- unusual driver loads

# comparison
|Type |needs user? |spreads automatically? | primary goal |
|-----|------------|-----------------------|--------------|
|Virus |yes |no |infect files |
|Worm |no |yes |spread rapidly |
|Trojan |yes |no |backdoor |
|Ransomware |yes |sometimes |encrypts files |
|Spyware |yes |no |steal data |
|Rootkit |no |no | hide malware |

# soc analyst mindset

when you see an alert, ask:
- is this malware delivery?
- is it persistence
- is it lateral movement?
- is data being exfiltrated?
- is this encryption behavior?

soc l1 is about:
- detect 
- validate
- escalate
