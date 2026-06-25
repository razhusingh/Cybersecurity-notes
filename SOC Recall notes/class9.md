# 30-Second Recall
- Hashing = One-way transformation of data into fixed-length output.
- Properties: One-way, Deterministic, Fixed Length, Avalanche Effect.
- MD5 & SHA1 = Weak/Broken.
- SHA256, SHA512 = Strong.
- bcrypt, Argon2 = Best for passwords.
- Passwords should be Hashed + Salted.
- Salt = Random value added before hashing.
- Pepper = Secret value stored outside database.
- Encryption = Reversible using a key.
- Hashing = Integrity.
- Encryption = Confidentiality.
- Symmetric Encryption = Same key.
- Asymmetric Encryption = Public Key + Private Key.
- HTTPS uses asymmetric encryption to exchange keys securely.


# Interview Questions

 Q1. What is hashing?

Answer: One-way mathematical transformation that converts data into a fixed-length output.

 Q2. What are the properties of hashing?

Answer: 
- One-way
- Deterministic
- Fixed output length
- Avalanche Effect

Q3. What is Avalanche Effect?

Answer: Small input change causes completely different hash output.

Q4. Why is MD5 insecure?

Answer: Vulnerable to collisions and rainbow table attacks.

Q5. What is salting?

Answer: Adding a random value to a password before hashing.

Q6. Why is salting important?

Answer: Prevents rainbow table attacks and identical hashes.

Q7. What is pepper?

Answer: Secret value stored outside database and added before hashing.

Q8. Hashing vs Encryption?

Answer:
- Hashing = One-way
- Encryption = Reversible with key

Q9. Why should passwords be hashed instead of encrypted?

Answer: Passwords only need verification, not decryption.

Q10. What is symmetric encryption?

Answer: Same key used for encryption and decryption.

Q11. What is asymmetric encryption?

Answer: Uses public and private key pair.

Q12. Examples of symmetric algorithms?

Answer: AES, ChaCha20.

Q13. Examples of asymmetric algorithms?

Answer: RSA, ECC, Diffie-Hellman.

Q14. What should SOC analysts check after a database breach?

Answer:
- Was hashing used?
- Was salting used?
- Which algorithm?
- bcrypt or MD5?

# Active Recall Flashcards
Flashcard 1

Q: Hashing purpose?
A: Integrity.

Flashcard 2

Q: Encryption purpose?
A: Confidentiality.

Flashcard 3

Q: Can hashing be reversed?
A: No.

Flashcard 4

Q: Can encryption be reversed?
A: Yes, with key.

Flashcard 5

Q: Best password hashing algorithms?
A: bcrypt, Argon2.

Flashcard 6

Q: Weak hashing algorithms?
A: MD5, SHA1.

Flashcard 7

Q: Salt meaning?
A: Random value added before hashing.

Flashcard 8

Q: Pepper meaning?
A: Secret value stored outside DB.

Flashcard 9

Q: Symmetric encryption uses how many keys?
A: One.

Flashcard 10

Q: Asymmetric encryption uses how many keys?
A: Two.

Flashcard 11

Q: HTTPS key exchange uses?
A: Public/Private key cryptography.

Flashcard 12

Q: Database stores what for authentication?
A: Username + Salt + Hash.

# Must Remember Points

✅ Hashing = Integrity
✅ Encryption = Confidentiality
✅ Passwords = Hash + Salt
✅ bcrypt > SHA256 for passwords
✅ Argon2 = Modern standard
✅ Salt prevents rainbow table attacks
✅ Pepper stored outside database
✅ MD5 & SHA1 should never be used for passwords
✅ HTTPS uses asymmetric encryption first, then secure session communication
✅ Weak password storage can lead to credential stuffing attacks

# SOC Analyst Mindset
During Database Breach Investigation

Ask:

1. Was password hashing used?
2. Which algorithm?
3. Was salting implemented?
4. Is pepper used?
5. Can attackers crack passwords quickly?
6. Is credential stuffing likely?

# Indicators After Password Dump
- Multiple login attempts
- Account takeover alerts
- Impossible travel alerts
- Password spray attacks
- Credential stuffing activity

# Root Cause to Remember

Weak password storage (MD5/SHA1 without salt) → Database breach → Password cracking → Credential stuffing → Account takeover


# Golden Line:
👉 Passwords = bcrypt/Argon2 + Salt (+ Pepper)
👉 Hashing = Integrity | Encryption = Confidentiality