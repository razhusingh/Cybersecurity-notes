# Windows editions
Different versions of windows exist forj different users
home -> basic users
pro -> business + security features
enterprise -> advanced security and management

# Windows Desktop (GUI)
GUI = Graphical User Interface
main components
>start menu
>taskbar
>desktop icons
>file explorer

important:
Attackers target users through GUI (malicious files, fake shortcuts,etc)

SOC monitors suspicious user activity.

# File system (NTFS)
New Technology File System
features:
>file permissions
>encryption
>compression
>access control

why important?
As pentester:
> check weak file permissions
> look for senstive files
As soc:
> monitor unauthorized file access

# Windows\system32 folder
location c:\windows\system32

contains:
> important system files
> DLL files
> Executables
> Admin tools
if attacker gets access here -> full control risk

# user accounts, profile and permissions
Types of accounts:
> administrator
> standard user
> guest

each user has:
c:\users\username

permissions:
> read 
> write
> execute
> full control
privilege escalation happens when user gets more access than allowed

# user accound control(UAC)
UAC prevents unauthorized admin changes.
when you see:
"Do you want to allow this app to make changes?"
that's UAC

As attacler"
> try to bypass UAC

As SOC:
> monitor suspicious elevation attempts

# control panel and settings
used to manage:
> network
> programs
> user accounts
> firewall
> system configuration

Attackers may:
> disable firewall
> add malicious programs

# Task manager
shortcut: ctrl + shift + esc

used to :
> view running processes
> stop applications
> check cpu / memory usage

soc uses this to:
> identify malware processes
pentesters check:
> what services are running

important commands to remember
> msconfig -> system configuration
> services.msc -> view services
> compmgmt.msc -> computer management
> taskmgr -> task manager
> regedit or regedt32 -> registry editor.
