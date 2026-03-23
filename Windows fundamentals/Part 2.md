# Windows fundamentals - part 2
(system configuration, UAC, computer management, registry,etc.)


# System configuration(msconfig)
what is it?
system configuration is used to:
- manage startup services
- boot options
- troubleshooting startup problems

why important for soc?
attackers often:
- add malicious services
- enable persistence via startup items

if you know msconfig ->
you can:
> identify suspicious startup services
> disable malicious boot entries

# Advanced system settings
path:
this pc -> paroperties -> advanced system settings

includes:
- performance settings
- environment variables
- startup and recovery
- remote settings

soc importance:
attackers may:
- modify environment variables
- enable remote connections
- cahnge startup behavior

you must always ask:
"why was this changed?"

# User account control(UAC)
what is UAC?
security feature that:
- prevents unauthorized admin changes
- promtps before privileged actions

why important?
malware tries to:
- disable UAC
- bypass UAC
- Run as admin silently

soc mindset:
is UAC is disabled -> Red flag

# computer management
run:
compmgmt.msc

contains:
- event viewer
- device manager
- disk management
- local users and groups
- shared folders

soc importance:
this is gold

you can:
> check failed logins
> check new users created
> check suspicious shares
> check disk tampering

if attacker created new admin user ->
you detect here.

# System information (msinfo32)
run:
msinfo32

shows:
os version
bios version
installed hardware
running servies

why important?
attackers gather system info before attacking

as soc:
if malware collects system info ->
you understand why.

# Resousrce monitor
run:
resmon

shows:
cpu usage
memory usage
disk activity
network activity

soc importance:
if:
- unknown process using high network
- strange ip connections
- suspicious memory usage

this helps identify malicious processes.

# command prompt
run: 
cmd

basic important commands:
ipconfig
whoami
net user
netstat
tasklist

why important?
attackers use cmd heavily.

if you dont know it -> you cant detect misuse

soc mindset:
know how attacker thinks in command line

# Registry editor
run :
regedit

what is registry?
database taht stores:
system settings
software configuration
startup programs

why important?
attackers:
> add persistence in registry
> modify registry for privilege escalation
> disable security tools

example loaction for startup persistence:
HKEY_LOCAL_MACHINE\Software\Microsoft\Windows\CurrentVersion\Run

soc mindset:
always check registry if system behaves weird

