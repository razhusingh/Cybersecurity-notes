# what is powershell
powershell is a windows command line shell and scripting language built on .net used for system administartion, automation and security investigation

key features:
- object based shell(not text based like bash)
- uses cmdlets
- supports scripting and pipelines
- widely used by system admins, soc analysts and attackers

example command:
get-command = lists all available commands

# powershell objects
powershell works with object instead of plain text.

each objext contains:
- property = information about object
- method = action object can perform

example:
get-process = returns objexts with properties like:
- name
- id
- cpu

# cmdlets
powershell commands are called cmdlets

format:
verb-noun

examples:
get-process = show processes
get-service = show services
get-content = read file
get-help = command help

example:
get-help get-service

# getting help
show command help:
get-help get-process

examples:
get-help new-localuser -examples

update help database:
update-help

# finding commands
list all commands:
get-command

commands starting with specific word:
get-command remove*

find alias:
get-alias echo

example output:
echo -> write-output

# powershell aliases
aliases are shortcut for commands

ls = get-childitem
cat = get-content
cd = set-location
echo = write-output

example:
ls

same as: get-childitem

# files system navigation
list files:
get-childitem or ls

change directory:
cd foldername

example:
cd c:\users

go back:
cd ..

current location:
pwd or get-location

# reading files
read file content:
get-content file.txt

example:
get-content raju.txt

alias:
cat file.txt

soc use: log file investigation

# searching inside files
use select-string

example:
select-string -path file.txt -pattern "password"

searches text inside files

equivalent of grep in linux

# piping
pipe sysmol (|)
pass output of one command to another

example:
get-process | sort-object cpu

meaning:
- get processes
- sort by cpu usage

# filtering data
use:
where-object

example:
get-childitem | where-object length -gt 100

show files greater than 100 bytes

example:
get-service | where-object {$_.status -eq "running"}

operators;
-eq = equal
-ne = not equal
-gt = greater than
-lt = less than
-like = pattern match

# sorting data
show results:
get-process | sort-object cpu

descending order:
get-process | soer-object cpu -descending

# system information
view processes:
get-process

view services:
get-services

select specific properties:
get-service | select name,displayname

network connections:
get-nettcpconnection

improtant property:
owning process

shows process responsible for connection

example:
get-nettcpconnection | select localaddress,localport,owningprocess

# file hash
used to verify file integrity

example:
get-filehash file.txt

common algorithms:
- SHA256
- MD5
- SHA1

# Service enumeration
list service:
get-service

search specific service:
get-service | where-object {$_.displayname -like "*raju*"}

# important properties

name = object name
displayname = service name
length = file size
status = service status
owningprocess = process responsible

# useful enumeration commands 
list users:
get-localuser

list groups:
get-localgroup

running processes:
get-process

installed programs:
get-wmiobject win32_product

system information:
systeminfo


# important commands (extra)
check command history:
get-history

check event logs:
get-eventlog -logname security

check running services:
get-service

check suspicious processes:
get-process

check network connections:
get-nettcpconnection

# quick summary
powershell is used for:
- system administration
- automation
- file management
- data filering
- security investigaton

it uses verb-noun cmdlets and object based pipeline system
