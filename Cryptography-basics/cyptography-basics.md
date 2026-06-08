# introduction
what is cryptography?
- cryptography is the practice of securing communication and data so that unauthorized parties cannot send or modify it. It forms the foundation of secure digital communication

# importance of cryptography
cryptography helps provide:
- confidentiality
- integrity
- authenticity
- authenticity

examples:
- secure website logins
- ssh conncetions
- online banking
- file integrity verification using hashes

# compliance standards mentioned
- pci dss (payment card industry data security standard)
- HIPAA (health insurance portability and accountability act)
- GDRP (general data protection regulation)
- DPA (data protection act)

# plaintext to ciphertext
plain text
- original readable data before encryption

examples:
- text
- images
- medical records
- credit card data

ciphertext
- encrypted form of plaintext

cipher
- algorithm or method to convert plaintext into ciphertext

key
- a string of bits the cipher uses to encrypt or decrypt data

encryption
- process of converting into ciphertext

decryption
- process of converting ciphertext back into plaintext

encryption flow
```
Plaintext
   ↓
Encryption + Key
   ↓
Ciphertext
   ↓
Decryption + Key
   ↓
Plaintext

```
# historical ciphers
caesar cipher
- one of the oldest encryption methods

how it works
- each letter is shifted by a fixed number

examples:
```
Plaintext : TRYHACKME
Key       : 3
Ciphertext: WUBKDFNPH
```
to decrypt:
- use the same key
- shift letters back

the caesar cipher is vulnerable to brute force because only a small number of shifts are possible

historical examples mentioned
- caesar cipher
- vigenere cipher
- enigma machine
- one time pad

# types of encryption
there are two main categories:

1. symmetric encryption
uses the same key for
- encryption
- decryption

also called: private key cryptography

challange
- the secret key must be shared securely

 DES(data encryption standard)
 - older symmetric encryption algorithm
 - uses 56 bit key
 
 3DES
 - this DES applied three times
 - the key size is 168 bits

 AES (advanced encryption standard)
 - modern replacement for DES was adopted in 2001
 - widely used today for secure encryption
 - ts key size can be 128,192 or 256 bits

2. Asymmetric encryption
uses two keys:
- public key
- private key

its also called: public key cryptography

# basic math
cryptography relies heavily on mathematics

XOR operation(^)
rule table
| A | B | A^B |
|---|---|-----|
|0 |0 |0 |
|0 |1 |1 |
|1 |0 |1 |
|1 |1 |0 |

what is : 1001 ^ 1010
- 0011

Modulo (%)
- returns the remainder after division

examples:
- 17 % 5 = 2


# important terms revision
| Term                  | Meaning                                |
| --------------------- | -------------------------------------- |
| Plaintext             | Original readable data                 |
| Ciphertext            | Encrypted data                         |
| Encryption            | Plaintext → Ciphertext                 |
| Decryption            | Ciphertext → Plaintext                 |
| Symmetric Encryption  | Same key for encrypt/decrypt           |
| Asymmetric Encryption | Public and private keys                |
| DES                   | Old symmetric cipher                   |
| AES                   | Modern symmetric cipher                |
| XOR                   | Bitwise operation used in cryptography |
| Modulo                | Mathematical remainder operation       |

# quick revision
```
Plaintext → Encryption → Ciphertext
Ciphertext → Decryption → Plaintext

DES = Old (Don't trust)
AES = Modern (2001)

Symmetric = One key
Asymmetric = Two keys

XOR:
1⊕1=0
1⊕0=1
0⊕1=1
0⊕0=0

PCI DSS = Credit card security standard
```
