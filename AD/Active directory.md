# Window domain
a group of user and computer under the administartor of given business

# Active directory 
active directory is a centralized directory service used in windows domains to manage users, computers and resources

 puprose
- provieds authentication and authorization
- stores information about objects
- enforces security policies

# domain controller (DC)
a domain controller is a server that runs active directory services

 Responsibilities
- authenticates users (login verification)

6
- authorizes access (permission control)
- enforces domain policies
- stores ad database

# authentication vs authorization
 authentication -> verifies identity (who are you?)
 authorization -> determines permissions(what can you access?)

# objects in active directory
objects are entities stored inside active directory

 common object types
- user
- group
- computer

important concept
each object has attributes(property)

example:
user -> username, password, email
computer -> machine name
group -> member list

# security principal
a security principal is any object that can be authenticated and assigned permissions

 types
user
group
computer

 key point
security principals recieve a SID

# SID (security identifier)
A SID is a unique identifier assigned to a security principal in windows

 important 
username can change
SID does not change
permissions are linked to sid not name

# organizational unit(ou)
an OU is a container used to organize objects within a domain

 purpose:
- logical grouping
- easier management
- apply specific policies (GPO)

OU is not a security principal 

# Active directory structure
'''text
domain: company.local
|
|------ OU: HR
|
|         |
|         |--- User: raju
|         |--- User: lone wolf
|         |
|
|
|------ OU: IT
|
|         |
|         |--- computer: pc-01
|         |--- computer: pc-02
|         |
|
|
|------ OU: finance
|         |
|         |--- USER: raju
|         |--- USER: raju2
|         |

A domain contains multiple organizational units(OUs) used to organize users and computers and apply group policies

# delegation
the process of granting privileges to a user over some ou or other AD object

Set-ADAccountPassword username -Reset -NewPassword (Read-Host -AsSecureString -Prompt 'New Password') -Verbose
Set-ADUser -ChangePasswordAtLogon $true -Identity sophie -Verbose

# managing users in active directory

Users represent accounts used by people or services to access network resources

purpose:
- allow login to dimain
- access network resources
- manage permissions centrally

user attributes:
- username
- password
- email
- departement
- group membership

important concept:
permissions should be assigned to groups instead of individual users

example:
HR group -> access HR folder
Employees -> added to HR group

# managing computers in active directory

computers joined to the domain are stored as computer objects.

Each computer has:
- computer account
- machine name
- security identifier (SID)

purpose:
- centralized device management
- apply security policies
- monitor network machines

example tasks:
- join computer to domain
- control login access
- apply group policy

# Group policy (GPO)

Group policy allows administrators to enforce configuration and security settings across users and computers.

important uses:
- enforces password policies
- disable USB devices
- configure firewall
- install software automatically
- control system settings

example:
- minimum password length = 12
- password expiry = 90 days

this policy automatically applies to all domain users.

# Authentication in active directory
Authentication verifies identity of the user before granting access

# main authentication protocols:

kerberos:
default authenticaiton protocol in active directory

features:
- ticket based authentication
- passwords not sent directly
- more secure than NTLM

simplified process:

user login
|
request ticket from domain controller
|
domain controller verifies identity
|
access granted

NTLM:
older authentication protocol

characteristics:
- less secure
- used for compatibility with older systems

# domain tree and forest
these define active directory strucutre in large organizations

Domain:
basic unit of active directory

example:
company.com

Tree:
collection of domains with the same namespace.

example:
company.com
sales.company.com
hr.company.com

Forest:
collection of multiple domain trees
highest level of AD structure

example:
company.com
anothercompany.com

both belong to the same forest

# trust relationships

trust allows users from one domain to access resources in another domain

example:
user from domain A can access resource in domain B

# Why active directory is important in cybersecurity

Active directory is a critical attack target in enterprise networks

Because it controls:
- authentication
- user accounts
- computers
- permissions
- security policies

if attacker compromises domain controller, they can control the entire
network

common AD attacks:
- credential dumping
- privilege escalation
- domain admin compromise

# Quick revision summary
active directory manages 
- users
- computers
- groups
- authentication
- policies
- domain structure

important components
- domain
- domain controller
- users
- groups
- computers
- organizational units
- group policy
- authentication
