# introduction
windows command prompt is a command line interface used to interact with windows using text commands instead of a graphical interface

it is useful for:
- system administration
- troubleshooting
- automation
- security investigations
- enumeration during penetration testing

open command prompt:-
cmd

# basic system information

1. whoami = shows the current logged in user

example output:-
desktop\user

use in cybersecurity:
- identify current privileges
- used during system enumeration

2. hostname = shows the computer name

useful for identifying the system in a network

3. systeminfo = displays detailed information about the system

important information gathered
- os version
- installed patches
- system architecture
- ram
- domain information

security use:
- os fingerprinting
- finding vulnerable windows versions

4. ver = displays windows version

# network troubleshooting

1. ipconfig = displays ip configuration

detailed version = ipconfig/all

shows:
- ipv4 address
- mac address
- dns servers
- default gateway

2. ping = tests network connectivity

ping google.com

used to check if a host is reachable

3. tracert = shows the path packets take to reach a destination

tracert google.com

useful for network troubleshooting

4. nslookup = queries dns to resolve domain names
ns lookup google.com

security use:
- dns investigation
- domain resolution

5. net user = lists system users

6. net localgroup = lists local groups

7. netstat = displays active network connections
netstat -ano
netstat -h, where -h displays the help page
netstat -abon
where,
- -a displays all established connections and listening port
- -b shows the program associated with established connections and listening port
- -o reveals the process id (pid)
- -n uses a numerical form for addresses and port numbers

important fields:
- local address
- remote address
- pid (process id)

security use:
- detect suspicious connections
- identify malware communication

# file and disk management

1. dir = lists files and directories
example,
dir c:\users

2. cd = changes directory
cd desktop

go back: cd ..

3. mkdir = creates a new directory
mkdir test

4. rmdir = removes a directory
rmdir test

5. copy = copies files
copy file.txt d:\backup

6. del = deletes files
del file.txt

# task and process management

1. tasklist = displays running processes
example output,
chrome.exe
explorer.exe

security use:
- identify suspicious processes
- malware detection

2. taskkill = terminates processes
kill by pid: taskkill /pid 1234 /f

kill by name: taskkill /IM chrome.exe /f

quick summary
- whoami = shows current user
- hostname = shows system name
- systeminfo = displays system information
- ifconfig = shows network configuration
- ping = tests connectivity
- tracert = shows packet route
- nslookup = dns query tool
- netstat = shows network connection
- dir = lists files
- cd = changes directory
- mkdir = creates folder
- del = deletes file
- tasklist = lists running processes
- taskkill = terminates processes


