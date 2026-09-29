# SOC Analyst L1 — Class 22
# Windows Active Directory

---

# 1. ⚡ 30-SECOND RECALL

## Active Directory

AD = centralized identity & access management.

    Authentication → Who are you?
    Authorization  → What can you access?

Structure:

    Objects → OUs → Domains → Trees → Forest

Physical:

    Domain Controller + Sites

Protocols:

    DNS → Find DC
    LDAP → Directory Search
    Kerberos → Authentication

Kerberos:

    TGT → Service Ticket → Resource Access

---

# 2. 🔥 MUST REMEMBER

## AD Objects

- Users
- Computers
- Printers
- Groups

## OU

    OU = Folder for organizing objects

## Domain

    Domain = Security Boundary

## Tree

    Group of related domains

## Forest

    Collection of trees

## Domain Controller

    Runs AD
    Stores AD database
    Database = ntds.dit

## GPO

    Group Policy Objects
    → Apply settings to many computers

## Sites

    Represent physical locations

---

# 3. 🔥 KERBEROS

    KDC
     ├── AS → TGT
     └── TGS → Service Ticket

### TGT

    Ticket Granting Ticket
    → Proves authentication

### Session Key

    Temporary key
    → Encrypts communication

### ⭐ IMPORTANT

    TGT ≠ Direct File Access

    TGT
      ↓
    Service Ticket
      ↓
    Resource Access

---

# 4. 🔥 KERBEROS 6 STEPS

    1. Request TGT
    2. TGT + Session Key
    3. Request Ticket + Auth
    4. Ticket + Session Key
    5. Request Service + Auth
    6. Server Authentication

              ↓
        Access Granted

---

# 5. 🔥 TGT vs SESSION KEY

| TGT | Session Key |
|---|---|
| Proves authentication | Secures communication |
| Usually ~10 hours | Short-lived |
| Only DC can read it | Client + Server |
| Used to request Service Ticket | Used to encrypt communication |

---

# 6. 🔥 AD ATTACKS

    Pass-the-Hash
    → NTLM Hash

    Kerberoasting
    → Steal Service Tickets

    Golden Ticket
    → Forge Kerberos Tickets

    DCSync
    → Steal Password Hashes from DC

    Privilege Escalation
    → User added to Domain Admins

---

# 7. 🔥 AD SOC EVENT IDs

    4624 → Login
    4625 → Failed Login
    4672 → Admin Privileges
    4720 → User Created
    4732 → User Added to Group

---

# 8. ⭐ INTERVIEW Q&A

### Q1. What is Active Directory?

A centralized system for managing identities, computers, resources and access in a Windows network.

### Q2. Authentication vs Authorization?

    Authentication → Who are you?
    Authorization  → What are you allowed to do?

### Q3. What is an OU?

A logical container used to organize AD objects.

### Q4. What is a Domain?

A main AD container and security boundary.

### Q5. What is a Forest?

A collection of AD trees.

### Q6. What is a Domain Controller?

A server that runs AD and stores the AD database.

### Q7. What is ntds.dit?

The Active Directory database file.

### Q8. What is Kerberos?

A ticket-based authentication protocol mainly used in Windows AD.

### Q9. What is a TGT?

Ticket Granting Ticket; proves that the user has authenticated and is used to request a Service Ticket.

### Q10. Does TGT directly provide file access?

No.

    TGT → Service Ticket → Resource Access

### Q11. What is Pass-the-Hash?

Using an NTLM hash instead of the password.

### Q12. What is Kerberoasting?

Stealing Kerberos service tickets.

### Q13. What is a Golden Ticket?

Forging Kerberos tickets.

### Q14. What is DCSync?

Stealing password hashes from the Domain Controller.

---

# 9. 🧠 SOC ANALYST MINDSET

Don't ask only:

    "What command ran?"

Ask:

    Why was it run?
    Who executed it?
    What did it access?
    Did it move laterally?

### Think:

    Identity
       ↓
    Authentication
       ↓
    Access
       ↓
    Activity
       ↓
    Lateral Movement

---

# 10. 📝 QUESTION PAPER MODE

1. What is Active Directory?
2. What are Authentication and Authorization?
3. What are AD Objects?
4. What is an OU?
5. What is a Domain?
6. What is a Tree?
7. What is a Forest?
8. What is a Domain Controller?
9. What is ntds.dit?
10. What are AD Sites?
11. What is Group Policy?
12. What are GPOs?
13. What is the role of DNS in AD?
14. What is the role of LDAP?
15. What is Kerberos?
16. What is KDC?
17. What is AS?
18. What is TGS?
19. What is a TGT?
20. What is a Session Key?
21. Does TGT directly provide file access?
22. What are the six Kerberos steps?
23. What is Pass-the-Hash?
24. What is Kerberoasting?
25. What is a Golden Ticket?
26. What is DCSync?
27. What is Event ID 4624?
28. What is Event ID 4625?
29. What is Event ID 4672?
30. What is Event ID 4720?
31. What is Event ID 4732?
32. What questions should a SOC analyst ask when investigating AD activity?

---

# 11. ✅ ANSWER KEY

1. Centralized identity and access management system for Windows networks.
2. Authentication verifies identity; Authorization determines permissions.
3. Users, Computers, Printers and Groups.
4. Logical container used to organize AD objects.
5. Main AD container/security boundary.
6. Group of related domains.
7. Collection of trees.
8. Server running Active Directory.
9. Active Directory database file.
10. Physical locations in an AD environment.
11. Feature for applying settings to many computers/objects.
12. Group Policy Objects.
13. Helps computers find the Domain Controller.
14. Used to search/lookup directory information.
15. Ticket-based authentication protocol used mainly in Windows AD.
16. Key Distribution Center.
17. Authentication Service.
18. Ticket Granting Service.
19. Ticket Granting Ticket.
20. Temporary key for secure communication.
21. No. A Service Ticket is required.
22. Request TGT → TGT + Session Key → Request Ticket + Auth → Ticket + Session Key → Request Service + Auth → Server Authentication.
23. Using an NTLM hash instead of the password.
24. Stealing Kerberos service tickets.
25. Forging Kerberos tickets.
26. Stealing password hashes from the Domain Controller.
27. Login.
28. Failed Login.
29. Admin Privileges.
30. User Created.
31. User Added to Group.
32. Why was it run? Who executed it? What did it access? Did it move laterally?

---

# 🔥 FINAL 10-SECOND RECALL

    AD
    ↓
    Identity + Access
    ↓
    Objects → OU → Domain → Tree → Forest
    ↓
    DC
    ↓
    DNS + LDAP + Kerberos
    ↓
    TGT
    ↓
    Service Ticket
    ↓
    Resource Access

    AD Attacks:
    Pass-the-Hash
    Kerberoasting
    Golden Ticket
    DCSync
    Privilege Escalation

    SOC IDs:
    4624 → Login
    4625 → Failed Login
    4672 → Admin
    4720 → User Created
    4732 → Group Added