# Project 1: Cryptographic Implementations

## Overview
This project consists of three cryptographic implementations using different cipher techniques:
1. **scrypt**: A stream cipher using a linear congruential keystream generator and a hashed key.
2. **vcrypt**: A stream cipher with an initialization vector (IV) to ensure unique ciphertexts for the same plaintext and key.
3. **feistel**: A Feistel block cipher operating on 128-bit blocks with 10 rounds of encryption using derived round keys.

Each script provides encryption and decryption functionality based on the provided password and file paths.

---

## Script Descriptions

### 1. **scrypt** (Stream Cipher)
This script implements a basic stream cipher using:
- A **Linear Congruential Generator (LCG)** to generate a keystream.
- The **SDBM hash function** to convert the password into a numeric seed.
- XOR encryption and decryption using the keystream.

**Usage:**
```
scrypt password plaintext ciphertext
scrypt password ciphertext plaintext
```
- Encrypts a plaintext file into ciphertext using a keystream derived from the password.
- Decrypts a ciphertext file back into plaintext using the same password.

**Key Features:**
- Uses XOR for encryption/decryption.
- Handles large files efficiently by processing data in chunks.
- Ensures consistent keystream generation from a given password.

---

### 2. **vcrypt** (Stream Cipher with IV)
This script extends the functionality of `scrypt` by introducing an **initialization vector (IV)** for added security.
- The IV ensures that encrypting the same plaintext with the same key generates different ciphertexts.
- The IV is stored as the first 8 bytes of the ciphertext file to facilitate decryption.

**Usage:**
```
vcrypt -e password plaintext ciphertext
vcrypt -d password ciphertext plaintext
```
- `-e`: Encrypts the plaintext file using a password-derived keystream and a random IV.
- `-d`: Decrypts the ciphertext file using the same password and the stored IV.

**Key Features:**
- Prevents identical plaintexts from producing identical ciphertexts.
- Uses XOR for encryption and decryption.
- Stores the IV in the output file for decryption reference.

---

### 3. **feistel** (Feistel Block Cipher)
This script implements a **10-round Feistel cipher** operating on **128-bit blocks** with **64-bit round keys**.
- Uses the **SDBM hash function** to generate the main encryption key.
- Derives **round keys** using an LCG.
- Applies a **custom Feistel round function** involving XOR, multiplication, and bit shifts.
- Uses **PKCS#7 padding** to ensure that plaintext sizes align with block sizes.

**Usage:**
```
feistel -e password plaintext ciphertext
feistel -d password ciphertext plaintext
```
- `-e`: Encrypts the plaintext file into ciphertext using Feistel network transformations.
- `-d`: Decrypts the ciphertext file back into plaintext by reversing the encryption rounds.

**Key Features:**
- Uses **Feistel structure** for reversible encryption.
- Encrypts and decrypts in **fixed 128-bit blocks**.
- Implements **PKCS#7 padding** to handle non-multiple block sizes.
- Processes data securely using **derived round keys**.

---

## Error Handling
Each script includes error handling for:
- Invalid or missing files.
- Permission issues when reading or writing files.
- Incorrect command usage.
- Password validation (must be a non-empty string).

