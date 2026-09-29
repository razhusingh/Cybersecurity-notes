# SOC Analyst L1 — Class 22
# Windows Active Directory 

---

# 1. Windows Active Directory

## What is Active Directory?

Active Directory (AD) can be thought of as the **brain/manager of a company's computer network**.

In a small home:

- One person may have one computer.
- The person can manually use their own username and password.

In a large company:

- Thousands of employees may use thousands of computers.
- Creating and managing every account separately on every computer would be difficult.

Active Directory solves this by providing a **centralized directory** where identities are stored and managed.

A user can use their centralized identity to log into computers within the company environment.

---

# 2. Core Concept — Identity & Access

At its heart, Active Directory performs two major functions:

## Authentication

Authentication means:

> Verifying who you are.

Example:

    User enters password
          ↓
    AD verifies identity
          ↓
    "Yes, this is John Doe"

## Authorization

Authorization means:

> Checking what you are allowed to access or do.

Example:

    John
      ↓
    Allowed → HR Printer
    Not Allowed → Finance Folder

### ⭐ Important

    Authentication = Who are you?
    Authorization = What are you allowed to do?

---

# 3. Active Directory — Main Building Blocks

The Active Directory diagram shows four major structural concepts:

    Objects
       ↓
    Organizational Units (OUs)
       ↓
    Domains
       ↓
    Forests & Trees

These form the logical organization of an AD environment.

---

# 4. Objects

Objects are the **building blocks** of Active Directory.

An object is a "thing" in the network.

Examples:

- Users
- Computers
- Printers
- Groups

## Users

Represent people who log into the network.

## Computers

Represent machines/workstations in the network.

## Printers

Represent network resources such as printers.

## Groups

Collections of users or computers used for simplified permissions.

### Simple Understanding

    User
    Computer
    Printer
    Group

    = AD Objects

---

# 5. Organizational Units (OUs)

## What is an OU?

Organizational Units (OUs) are logical containers used to organize objects.

Think of an OU as a **folder**.

Objects can be placed inside OUs for easier management.

Examples:

    Accounting OU
        ↓
    Accounting Users
    Accounting Computers

    Sales OU
        ↓
    Sales Users
    Sales Computers

OUs help organize objects and make administration easier.

---

# 6. Domains

A **Domain** is the main security container in Active Directory.

It acts as a **security boundary**.

A domain contains:

- Objects
- Policies
- Administrative structure

Example:

    corp.apple.com

Everything inside the domain follows the rules associated with that domain.

---

# 7. Trees

A **Tree** is a group of domains that share the same naming structure.

Example:

    apple.com
       ├── sales.apple.com
       └── uk.apple.com

These domains can belong to the same `apple.com` tree.

### Remember

    Tree = Group of related domains
           sharing the same namespace

---

# 8. Forests

A **Forest** is the highest-level structure shown in the Active Directory hierarchy.

It is a collection of trees.

Example:

    Forest
      ├── apple.com Tree
      │     ├── sales.apple.com
      │     └── uk.apple.com
      │
      └── beats.com Tree

If Apple acquired another company called Beats, the `apple.com` and `beats.com` trees could exist within one forest and communicate with each other.

### 🔥 Remember

    Domain
       ↓
    Tree
       ↓
    Forest

---

# 9. Active Directory Logical Structure

The AD ecosystem can be viewed as two major areas:

## Zone 1 — Hierarchy & Physical Structure

Includes:

- Forest
- Tree
- Domain
- Organizational Unit (OU)

## Zone 2 — Objects & Policies

Includes:

- Users
- Computers
- Printers
- Groups
- Group Policy

---

# 10. Group Policy

## What is Group Policy?

Group Policy is one of the powerful features of Active Directory.

It allows administrators to change settings for **many computers at once**.

Group Policy Objects are called:

    GPOs

---

# 11. Group Policy Objects (GPOs)

A GPO can define settings and rules for objects in:

- OU
- Domain
- Site

Examples of settings shown in the diagram:

- Desktop Wallpaper
- Password Policy
- Lock Screen

## Example

An administrator can create a rule:

> Every computer in the Sales department should use the company wallpaper and lock the screen after 5 minutes of inactivity.

Without AD:

    Administrator
        ↓
    Computer 1
        ↓
    Computer 2
        ↓
    Computer 3
        ↓
    ...
    Thousands of computers

With AD:

    Administrator
        ↓
    GPO
        ↓
    Applies settings to many computers

---

# 12. How AD Components Work Together

The Active Directory diagram shows this flow:

    Administrators create OUs
              ↓
    Objects are placed into OUs
              ↓
    Group Policies are applied to OUs
              ↓
    Domain Controllers enforce policies

---

# 13. Active Directory Physical Structure

The logical structure describes **how AD is organized**.

The physical structure describes **where the AD data actually lives**.

The two important physical concepts are:

- Domain Controllers
- Sites

---

# 14. Domain Controller (DC)

A **Domain Controller (DC)** is the server that runs Active Directory.

It:

- Runs the AD software
- Holds the Active Directory database
- Handles authentication-related requests

The AD database is stored in:

    ntds.dit

## Authentication Example

    User enters password
          ↓
    Computer communicates with DC
          ↓
    DC checks the identity
          ↓
    Authentication result

---

# 15. Sites

An Active Directory **Site** represents a physical location.

Examples:

    New York Office
    London Office

Sites help AD use an appropriate nearby server.

Example:

    User in London
          ↓
    London Server

instead of unnecessarily communicating with a distant:

    New York Server

This helps avoid slow communication caused by unnecessary distance.

---

# 16. Three Main Protocols / "Languages" Used by AD

Active Directory relies on three important protocols/concepts shown in the PDF:

1. DNS
2. LDAP
3. Kerberos

---

# 17. DNS — Domain Name System

DNS acts like the **GPS** for Active Directory.

It helps computers locate the:

    Domain Controller

on the network.

Simple flow:

    Computer
       ↓
    DNS
       ↓
    Find Domain Controller
       ↓
    Communicate with DC

---

# 18. LDAP — Lightweight Directory Access Protocol

LDAP is the **directory search language**.

It is used to look up information in Active Directory.

Example:

    Find the email address
    for Jane Smith

LDAP helps retrieve directory information.

---

# 19. Kerberos

Kerberos is the **ticket-based authentication protocol** used mainly in Windows Active Directory environments.

It uses tickets instead of repeatedly sending the user's password when accessing resources.

Main concepts:

- KDC
- Authentication Service (AS)
- Ticket Granting Service (TGS)
- TGT
- Service Ticket
- Session Key

---

# 20. Active Directory Simple Analogy

| AD Term | Simple Analogy |
|---|---|
| Object | A single contact in your phone |
| OU | A folder such as "Work Contacts" |
| Domain | Your entire phone's contact list |
| Forest | Multiple phones synced together |
| Domain Controller | The actual phone hardware storing the data |

---

# 21. Kerberos — Basic Concept

Kerberos can be understood as the **security guard of Active Directory**.

It uses a ticket system.

Instead of repeatedly providing your password when accessing resources, Kerberos provides tickets that prove your identity and allow access.

---

# 22. The Three Main Players in Kerberos

The PDF uses a theme-park analogy.

## 1. Client — "You"

The client is the user/computer trying to:

- Log in
- Access a file
- Access a printer

## 2. Domain Controller / KDC — "Ticket Office"

The KDC is the place that handles Kerberos authentication.

It contains two important services:

- AS — Authentication Service
- TGS — Ticket Granting Service

## 3. Resource Server — "The Ride"

The resource server is the server containing the resource you want to access.

Examples:

- File Server
- Printer

---

# 23. KDC — Key Distribution Center

KDC stands for:

    Key Distribution Center

It is the "Ticket Office" in the analogy.

The KDC contains:

- Authentication Service (AS)
- Ticket Granting Service (TGS)

---

# 24. Authentication Service (AS)

The:

    AS = Authentication Service

The AS provides the initial authentication process and issues the:

    TGT
    Ticket Granting Ticket

Analogy:

    AS = Gives you the wristband
          at the entrance

---

# 25. Ticket Granting Service (TGS)

The:

    TGS = Ticket Granting Service

The TGS provides a:

    Service Ticket

when the user wants to access a particular service/resource.

Analogy:

    TGS = Gives you the ticket
          for a specific ride

---

# 26. TGT — Ticket Granting Ticket

## What is a TGT?

TGT stands for:

    Ticket Granting Ticket

The PDF describes it as a **master pass / wristband**.

It proves that the user has already authenticated.

## What the TGT Contains

The PDF shows that the TGT contains:

- User ID
- IP Address
- Expiration / Valid-until timestamp

The example shown gives a validity period of approximately:

    10 hours

## Encryption

The TGT is encrypted by the Domain Controller using a secret key known only to the Domain Controller.

Therefore, the user cannot simply open or modify the TGT.

---

# 27. Purpose of TGT

The TGT proves:

    "I have already authenticated."

It is later presented when requesting access to services.

### ⭐ Important

A TGT **does NOT directly give access to files or printers**.

The TGT allows the user to communicate with the ticket service and request a:

    Service Ticket

for the required resource.

---

# 28. Session Key

A **Session Key** is a temporary, disposable key used for secure communication.

The PDF compares it to a:

    Secret Handshake

It is created for a particular communication/session.

## Purpose

The Session Key is used to:

- Secure communication
- Encrypt messages
- Prevent eavesdropping

The client and server both receive a copy.

---

# 29. Why Session Keys Are Used

Suppose:

    Client ↔ Server

communicate over a network.

An attacker may try to listen to the communication.

The real password should not be repeatedly used to protect those messages.

Instead:

    Domain Controller
          ↓
    Creates Session Key
          ↓
    Client receives copy
          +
    Server receives copy
          ↓
    Secure communication

---

# 30. Session Key Characteristics

The Session Key is:

- Random
- Temporary
- Disposable
- Used for secure communication

The PDF states that even if a Session Key is stolen, it expires after a short period, so the user's real password remains safe and untouched.

---

# 31. TGT vs Session Key

| Feature | TGT | Session Key |
|---|---|---|
| Analogy | Wristband | Secret Handshake |
| Created by | Domain Controller (KDC) | Domain Controller (KDC) |
| Who can read it? | Only Domain Controller | Client and Server |
| Purpose | Proves user is already logged in | Encrypts communication |
| Lifespan | Usually around 10 hours | Very short / often expires after task |

### 🔥 Remember

    TGT
    ↓
    Proof of Authentication

    Session Key
    ↓
    Secure Communication

---

# 32. The "Two Envelope" Trick

When the Domain Controller sends the response during the initial authentication process, the response contains two important pieces.

## Envelope A — TGT

The TGT is locked/encrypted.

The user cannot open it.

The user simply keeps it and later presents it to the ticket service.

## Envelope B — Session Key

The Session Key is protected using a key derived from the user's password.

Because the user knows the password, the user can obtain the Session Key.

---

# 33. Important TGT Mistake to Avoid

A common mistake is thinking:

    TGT = Direct File Access

This is incorrect.

Correct understanding:

    TGT
      ↓
    Proves authentication
      ↓
    Used to request Service Ticket
      ↓
    Service Ticket
      ↓
    Access specific resource

So:

    TGT ≠ Direct File Access

---

# 34. Kerberos Authentication — 6-Step Process

The PDF's Kerberos diagram shows six major steps.

    1. Request TGT
    2. TGT + Session Key
    3. Request Ticket + Auth
    4. Ticket + Session Key
    5. Request Service + Auth
    6. Server Authentication

---

# 35. Step 1 — Request TGT

The user provides their credentials.

The computer sends an authentication request to the Domain Controller / Authentication Service.

Conceptually:

    User
      ↓
    Authentication Request
      ↓
    Authentication Service

The user is asking:

    "I am John. Here is proof of my identity."

---

# 36. Step 2 — TGT + Session Key

The Authentication Service checks whether the user exists in the database.

If the user is legitimate:

    Authentication Service
          ↓
    TGT + Session Key
          ↓
    Client

The TGT acts like the user's entry wristband.

It proves the user successfully authenticated.

---

# 37. Step 3 — Request Ticket + Authentication

The user wants to access a resource.

Example:

    Finance Spreadsheet

The user sends a request to the:

    TGS

The request includes authentication information and the TGT.

Conceptually:

    Client
      ↓
    TGT + Authentication
      ↓
    TGS

The user is effectively saying:

    "I have my wristband.
     I want a ticket for this resource."

---

# 38. Step 4 — Ticket + Session Key

The TGS checks the request and determines whether the user can access the requested service.

If allowed:

    TGS
      ↓
    Service Ticket + Session Key
      ↓
    Client

The Service Ticket is specific to the requested service/resource.

---

# 39. Step 5 — Request Service + Authentication

The client contacts the desired resource server.

Example:

    Finance Server

The client presents:

    Service Ticket

Conceptually:

    Client
      ↓
    Service Ticket + Authentication
      ↓
    Resource Server

---

# 40. Step 6 — Server Authentication

The resource server checks the ticket.

If the ticket is valid and was issued by the official ticket authority:

    Resource Server
          ↓
    Authentication Successful
          ↓
    Access Granted

The user can now access the requested resource.

---

# 41. Complete Kerberos Flow

    USER / CLIENT
          │
          │ 1. Request TGT
          ↓
    AUTHENTICATION SERVICE
          │
          │ 2. TGT + Session Key
          ↓
    CLIENT
          │
          │ 3. Request Ticket + Auth
          ↓
    TICKET GRANTING SERVICE
          │
          │ 4. Service Ticket + Session Key
          ↓
    CLIENT
          │
          │ 5. Request Service + Auth
          ↓
    RESOURCE SERVER
          │
          │ 6. Server Authentication
          ↓
      ACCESS GRANTED

---

# 42. Kerberos Detailed Flow

The detailed diagram shows these components:

- Users
- Ticket Granting Service
- Authentication Service
- Kerberos Database
- Service Server

Flow:

    User sends authentication request
                ↓
    Authentication Service
                ↓
    Checks whether user exists in database
                ↓
    Issues TGT
                ↓
    User sends request to TGS
                ↓
    TGS checks whether user exists in database
                ↓
    TGS issues Service Ticket
                ↓
    User contacts desired Service Server
                ↓
    Service Ticket is presented
                ↓
    Access granted

---

# 43. Why Kerberos Is Used

## Security

The user's actual password is only used at the beginning of the authentication process.

After that:

    Password
       ↓
    Tickets
       ↓
    Service Access

This reduces the need to repeatedly send the password across the network.

If someone is listening to network traffic, they see temporary tickets rather than repeatedly seeing the user's actual password.

## Speed / Convenience

After receiving the TGT, the user does not need to type the password again every time they access another supported resource.

Example:

    One TGT
       ↓
    File 1
    File 2
    File 3
    Printer 1
    Printer 2
    ...
    
The PDF explains that the user can access many resources without repeatedly typing the password.

---

# 44. Kerberos Authentication Summary

    Password / Identity
          ↓
    Authentication Service
          ↓
    TGT + Session Key
          ↓
    TGS
          ↓
    Service Ticket
          ↓
    Resource Server
          ↓
    Access Granted

---

# 45. Active Directory Attacks

The PDF lists five important Active Directory attacks/techniques.

## 1. Pass-the-Hash

Attackers use an:

    NTLM Hash

instead of the actual password for authentication.

### Key Point

    Password
       ↓
    NTLM Hash
       ↓
    Attacker uses hash

---

# 46. Kerberoasting

Kerberoasting involves:

    Stealing Kerberos Service Tickets

The attacker targets Kerberos service tickets that can potentially be used in an attack.

### Key Point

    Kerberos
       ↓
    Service Ticket
       ↓
    Steal / Attack Ticket
       ↓
    Kerberoasting

---

# 47. Golden Ticket

Golden Ticket attack involves:

    Forging Kerberos Tickets

The attacker creates a forged Kerberos ticket to impersonate a valid identity.

### Key Point

    Kerberos
       ↓
    Forged Ticket
       ↓
    Unauthorized Authentication

---

# 48. DCSync

DCSync involves:

    Stealing Password Hashes
    from the Domain Controller

The attacker abuses directory replication-related functionality to obtain credential information.

### Key Point

    Domain Controller
          ↓
    Password Hashes
          ↓
    DCSync
          ↓
    Steal Hashes

---

# 49. Privilege Escalation in AD

An example shown in the PDF:

    User
      ↓
    Added to Domain Admins
      ↓
    Higher Privileges

Adding a user to a highly privileged group such as:

    Domain Admins

is an important security event to investigate.

---

# 50. AD Logs — SOC Important

The PDF identifies these important Active Directory Event IDs:

| Event ID | Meaning |
|---|---|
| 4624 | Login |
| 4625 | Failed Login |
| 4672 | Admin Privileges |
| 4720 | User Created |
| 4732 | User Added to Group |

---

# 51. Event ID 4624

    4624 → Login

Indicates a successful login.

SOC can use it to understand:

- Who logged in
- When the login occurred
- The authentication activity

---

# 52. Event ID 4625

    4625 → Failed Login

Indicates a failed login attempt.

SOC can investigate repeated failed logins for suspicious authentication activity.

---

# 53. Event ID 4672

    4672 → Admin Privileges

Indicates special/admin privileges being assigned during a logon.

This is important when investigating privileged account activity.

---

# 54. Event ID 4720

    4720 → User Created

Indicates that a new user account was created.

SOC should investigate unexpected account creation.

---

# 55. Event ID 4732

    4732 → User Added to Group

Indicates a user was added to a group.

This is particularly important when the group provides elevated privileges.

---

# 56. AD for SOC — Investigation Mindset

When investigating Active Directory activity, do not ask only:

    "What command ran?"

Instead ask:

### Why was it run?

Understand the purpose of the activity.

### Who executed it?

Identify the user/account responsible.

### What did it access?

Determine what resources were accessed.

### Did it move laterally?

Determine whether the activity spread to other systems.

---

# 57. Final SOC Investigation Questions

    WHO?
      ↓
    Why was it run?
      ↓
    Who executed it?
      ↓
    What did it access?
      ↓
    Did it move laterally?

This helps the SOC analyst understand the complete activity instead of focusing only on a single command.

---

# 58. Active Directory — Complete Structure

    ACTIVE DIRECTORY
          │
          ├── Objects
          │     ├── Users
          │     ├── Computers
          │     ├── Printers
          │     └── Groups
          │
          ├── Organizational Units
          │     ├── Accounting
          │     └── Sales
          │
          ├── Domain
          │
          ├── Tree
          │
          └── Forest

---

# 59. AD Physical Structure

    DOMAIN CONTROLLER
          ↓
    Runs Active Directory
          ↓
    Stores AD Database
          ↓
    ntds.dit

    SITES
      ↓
    Represent Physical Locations
      ↓
    Help users communicate with
    appropriate nearby servers

---

# 60. AD Protocols

    DNS
    ↓
    Finds Domain Controller

    LDAP
    ↓
    Searches Directory Information

    Kerberos
    ↓
    Ticket-Based Authentication

---

# 61. Kerberos Memory Map

    KDC
    ├── AS
    │    ↓
    │   TGT
    │
    └── TGS
         ↓
      Service Ticket
         ↓
    Resource Server
         ↓
      Access

---

# 62. TGT vs Service Ticket

    TGT
      ↓
    Proves you are authenticated
      ↓
    Used to request service ticket

    Service Ticket
      ↓
    Specific to requested service
      ↓
    Used to access resource

### 🔥 MUST REMEMBER

    TGT ≠ Direct File Access

    TGT → Get Service Ticket
    Service Ticket → Access Resource

---

# 63. AD Attack Memory Map

    Pass-the-Hash
    → NTLM Hash

    Kerberoasting
    → Kerberos Service Tickets

    Golden Ticket
    → Forge Kerberos Tickets

    DCSync
    → Steal Password Hashes from DC

    Privilege Escalation
    → User Added to Domain Admins

---

# 64. AD SOC Event ID Memory

    4624 → Login
    4625 → Failed Login
    4672 → Admin Privileges
    4720 → User Created
    4732 → User Added to Group

---

# 65. ⭐ SOC Mindset

When investigating Active Directory:

    Don't ask only:
    "What command ran?"

    Ask:

    Why was it run?
          ↓
    Who executed it?
          ↓
    What did it access?
          ↓
    Did it move laterally?

---

# 66. ⭐ Key Concepts to Understand

## Authentication

    Prove identity

## Authorization

    Determine permissions

## Object

    User / Computer / Printer / Group

## OU

    Logical container for objects

## Domain

    Security boundary

## Tree

    Group of related domains

## Forest

    Collection of trees

## Domain Controller

    Server running Active Directory

## Site

    Physical location

## DNS

    Helps locate Domain Controller

## LDAP

    Directory lookup/search

## Kerberos

    Ticket-based authentication

## TGT

    Master authentication ticket

## Session Key

    Temporary key for secure communication

## Service Ticket

    Ticket used to access a specific service

---

# 67. 🔥 Final Active Directory Attack Story

    User Authentication
          ↓
    Domain Controller
          ↓
    Kerberos
          ↓
    TGT
          ↓
    Service Ticket
          ↓
    Resource Access

Potential attacker activity:

    Credential Abuse
          ↓
    AD Attack
          ↓
    Privilege Escalation
          ↓
    Resource Access
          ↓
    Lateral Movement

---

# 68. FINAL MEMORY MAP

    ACTIVE DIRECTORY
          ↓
    Identity + Access
          ↓
    Authentication + Authorization
          ↓
    Objects
          ↓
    OUs
          ↓
    Domains
          ↓
    Trees
          ↓
    Forest
          ↓
    Domain Controller
          ↓
    DNS + LDAP + Kerberos
          ↓
    Kerberos Authentication
          ↓
    TGT
          ↓
    Service Ticket
          ↓
    Resource Access
          ↓
    SOC Monitoring
          ↓
    AD Attack Detection

---
