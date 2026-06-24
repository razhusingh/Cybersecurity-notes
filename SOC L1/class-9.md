# Hashing, Salting, and Encryption

what is hashing?
- A hash is a one-way mathematical transformation of data into a fixed length string

- think of it like: 
input -> hash function -> fixed length output

- if password is :
password123

- using MD5 it becomes:
482c811da5d5b4bc6d497ffa98491e38

no matter how long input is -> output length is fixed

 properties of hashing
- one-way (cannot reverse easily)
- deterministic (same input -> same output)
- fixed output length
- small input change -> completely different output

example:
- password234
- password123

completely different hashes

this is called the Avalanche effect

# common hash Algorithms
|algorithm | secure today? | notes |
|----------|---------------|-------|
|MD5 |no |very weak |
|SHA1 |no |broken |
|SHA256 |yes |strong |
|SHA512 |yes |strong |
|bcrypt |very strong |designed for passwords |
|Argon2 |very strong |modern standard |

# why hash passwords?
imagine a website stores passwords in plain text:

- username: raju
- password: raju@123

if database is hacked -> attacker sees everyting

instead, website stores:
- username: raju
- hash: 3jr354u3ip3...

even if database leaks -> attacker must crack hash first

# the big problem (without salting)
hashing alone is not enough because:
- if two users use same password:
user1 -> password123
user2 -> password123

both hashes will be identical

attacker instantly knows:
- they share same password

# Rainbow table attack
attacker create huge precomputed tables like:
|password |hash |
|---------|-----|
|123456 |e10dkd844kds4... |
|password |hsfjk343k43434k12k..|
|admin123 |jdf43dfa3459deic.. |

if database hash matches one in table -> password instantly cracked 

this is why MD5/SHA1 are dangerous

# what is salting
salt = random value added to password before hashing

- instead of hashing:
password123

- system hashes:
password123 + random salt

example
- user password 
password123

- salt generated
x3v4b5

- system hashes:
password123x3v4b5

- output:
a43dk39ld9..

another user with same password gets different salt -> different hash

# why salting is powerful

even is 100 users use same password:

without salt:
- same hash

with salt:
- all different hashes

attacker cannot use rainbow tables effevtively

they must brute force each hash individually

this makes cracking extermely expensive

# how salting is stored

database stores:
- username
- salt
- hash

when user logs in:
- 1. system retrieves salt
- 2. adds salt to entered password
- 3. hashes it
- 4. compares with stored hash

if match -> login success

# soc perspective: why you must understnad this
during incident response:

if database leaked, you must assess:
- was hashing used?
- was salting used?
- which algorithm?
- was it bcrypt or just MD5?

if weak hashing -> high risk of credential stuffing later.

1. Company stores passwords in MD5 without salt
2. Database breached
3. Attacker cracks hashes in minutes
4. Users reuse same password on:
○ Email
○ VPN
○ Banking
5. Massive credential stuffing campaign begins

SOC sees:

● Login attempts from multiple IPs
● Account takeovers
● Impossible travel alerts

Root cause?
 Weak hashing practice

 # advanced concept: pepper
pepper = secret value stored outside database(eg. server config)

instead of: 
- password + salt

it becomes:
- password + salt + pepper

even if database leaks -> attacker doesn't know pepper

extra layer of protection

# what is Encryption?
Encryption is the process of converting readable data (plaintext) into unreadable data (ciphertext) using a cryptographic key, so that only authorized parties can read it

Basic flow:
- plaintext -> encryption algorithm + key -> ciphertext
- ciphertext -> decryption algorithm + key -> plaintext

so encryption is reversible if you have the correct key

Example
- original message:
bank transfer = 50,000

- encrypted message (ciphertext):
a12k3d5k85b9

with the correct key, it can be decrypted back to the original message

# why encryption is used
Encryption protects data confidentiality, meaning only authorized users can read the data

common uses:
- HTTPS Website traffic
- vpn communication
- disk encryption
- secure messaging
- file encryption
- database encryption
- email encryption

# Types of encryption
1. symmetric encryption
- uses one single key for both encryption and decryption

- example:
 plaintext + secretkey -> ciphertext
 ciphertext + secretkey -> plaintext

 Example uses:
 - disk encryption
 - vpn tunnels
 - file encryption

problem: key sharing must be secure

popular algorithms:
|algorithm |use |
|----------|----|
|AES |most common modern encryption |
|DES |Old and insecure |
|3DES |legacy |
|chacha20 |modern secure encryption |

2. Asymmetric encryption (public key cryptography)

Uses two keys:
- public key (shared with everyone)
- private key (kept secret)

process:
- public key -> encrypt
- private key -> decrypt

example uses:
- https websites
- ssl/tls handshake
- email encryption(PGP)

popular algorithms:
|Algorithm |use |
|----------|----|
|RSA |SSL/TLS |
|ECC |modern secure communications |
|Diffie-Hellman |key exchange |

# HTTPs example: Encryption 
when you visit a website:
- browser -> server

steps:
1. browser gets public key from server
2. browser encrypts session key
3. server decrypts using private key
4. secure communications begins

that's how HTTPs works

# hashing vs encryption (very important differnce)
|Feature |Encryption |Hashing |
|--------|-----------|--------|
|Reversible |yes |
|uses key |yes |no |
|purpose |protect data confidentiality |verify data integrity |
|output length |variable |fixed |
|example use |HTTPs traffic |password storage |
|can original data be retrieved |yes |no |

# soc analyst perspective
understanding this helps in
- investigating data breaches
- analyzing password dumps
- understanding credential theft
- investigating encrypted traffic

Example soc question:

if attacker steal:
- encrypted database -> harder to access
- hashed password -> may crack offline

