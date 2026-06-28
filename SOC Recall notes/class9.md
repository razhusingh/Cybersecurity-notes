# 30-Second Recall (Day 9 – Hashing & Encryption)
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

# Must Remember Points

- Hashing = Integrity
- Encryption = Confidentiality
- Passwords = Hash + Salt
- bcrypt > SHA256 for passwords
- Argon2 = Modern standard
- Salt prevents rainbow table attacks
- Pepper stored outside database
- MD5 & SHA1 should never be used for passwords
- HTTPS uses asymmetric encryption first, then secure session communication
- Weak password storage can lead to credential stuffing attacks

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
- Passwords = bcrypt/Argon2 + Salt (+ Pepper)
- Hashing = Integrity | Encryption = Confidentiality

#  Question Paper Mode
1. What is Hashing?

2. What are the four properties of Hashing?

3. What is the Avalanche Effect?

4. Name common hash algorithms and identify which are secure today.

5. Why should passwords be hashed instead of encrypted?

6.What is a Rainbow Table Attack?

7. Why is hashing alone not enough for password protection?

8. What is Salting and why is it important?

9. What is Pepper and how is it different from Salt?

10. Explain the password verification process using Salt.

11. From a SOC Analyst's perspective, what should be checked after a password database breach?

12. What is Encryption?

13. Why is Encryption used?

14. What is Symmetric Encryption? Name two algorithms.

15. What is Asymmetric Encryption? Name two algorithms.

16. Explain how HTTPS uses both Symmetric and Asymmetric Encryption.

17. What is the difference between Hashing and Encryption?

18. Compare Symmetric Encryption and Asymmetric Encryption.

19. Why are MD5 and SHA1 considered insecure?

20. Explain a real-world credential stuffing attack caused by weak password hashing.

21. Which encryption method is faster: Symmetric or Asymmetric?

22. Which encryption method is mainly used for key exchange in HTTPS?

23. Which hashing algorithms are recommended for password storage?

24. Can hashed data be reversed? Can encrypted data be reversed?

25.Explain the difference between Integrity and Confidentiality.

# Answer Key

1. Hashing is a one-way mathematical transformation that converts data into a fixed-length hash value.

2.
```
One-way
Deterministic
Fixed output length
Avalanche Effect
```
3. A small change in input produces a completely different hash output.

4.
```
MD5 – Insecure
SHA1 – Insecure
SHA256 – Secure
SHA512 – Secure
bcrypt – Very Secure
Argon2 – Modern Standard
```
5. Because hashing is one-way and protects password integrity, while encryption is reversible using a key. Passwords should be hashed and salted, not encrypted.

6. An attack that uses precomputed hash tables to recover plaintext passwords from stolen password hashes.

7. Identical passwords produce identical hashes, making Rainbow Table attacks possible.

8. Salt is a unique random value added before hashing to produce different hashes for identical passwords and defend against Rainbow Table attacks.

9. Salt is stored with the hash and is unique for every user. Pepper is a secret value stored separately from the database and adds an extra security layer.

10. User enters password → Retrieve stored salt → Add salt to password → Hash → Compare with stored hash → Login if matched.

11.
```
Was hashing used?
Was salting used?
Which algorithm was used?
Was bcrypt/Argon2 or weak MD5/SHA1 used?
```
12. Encryption converts readable plaintext into unreadable ciphertext using a cryptographic key and can be reversed with the correct key.

13. To protect data confidentiality during storage and transmission. Common uses include HTTPS, VPNs, file encryption, email encryption and database encryption.

14. Symmetric Encryption uses the same key for encryption and decryption. Examples: AES, ChaCha20.

15. Asymmetric Encryption uses a public key for encryption and a private key for decryption. Examples: RSA, ECC.

16. HTTPS uses Asymmetric Encryption to exchange the session key securely, then Symmetric Encryption (such as AES) to encrypt the communication.

17.
```
Hashing → One-way, Integrity, No key, Password storage.
Encryption → Reversible, Confidentiality, Uses key, Data protection.
```
18.
```
Symmetric → One key, Faster.
Asymmetric → Two keys, Slower, Used for secure key exchange.
```
19. They are vulnerable to collisions and Rainbow Table attacks, making them unsuitable for secure password storage.

20. Weak hashing (such as MD5 without salt) → Database breach → Passwords cracked → Users reuse passwords → Credential Stuffing → Account takeovers.

21. Symmetric Encryption.

22. Asymmetric Encryption.

23. bcrypt and Argon2.

24.
```
Hashing → Cannot be reversed.
Encryption → Can be reversed with the correct key.
```
25.
```
Integrity: Ensures data has not been modified (Hashing).
Confidentiality: Ensures only authorized users can read the data (Encryption).
```
