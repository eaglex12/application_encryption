Encryption and Decryption Process Overview

This document explains the encryption and decryption process used in the EncryptionService implemented with NestJS, utilizing the AES-256-CBC algorithm.

1. **Encryption Process:**

   a. **Algorithm**: The encryption uses the AES-256-CBC (Advanced Encryption Standard with a key size of 256 bits and Cipher Block Chaining mode) which is a symmetric encryption algorithm. This means the same key is used for both encryption and decryption.

   b. **Key Generation**: The encryption key is a critical component and should be kept secure. In this implementation, the key is read from environment variables as a 64-character hexadecimal string representing a 32-byte key.

   c. **Initialization Vector (IV)**: For each encryption operation, a unique IV is generated. The IV is a random 16-byte value that ensures that the same plaintext encrypts to different ciphertexts each time, enhancing security by preventing patterns in encrypted data.

   d. **Encrypting Data**: The `encrypt` method performs the following steps:
      - It takes the plaintext (the data to be encrypted) as input.
      - A random IV is generated for the encryption.
      - The data is encrypted using the AES-256-CBC algorithm with the provided key and generated IV.
      - The method returns an object containing both the IV and the encrypted data in hexadecimal format.

2. **Decryption Process:**

   a. **Receiving Encrypted Data**: The decryption process requires both the IV and the encrypted data. The IV must match the one used during encryption to successfully retrieve the original plaintext.

   b. **Decrypting Data**: The `decrypt` method performs the following steps:
      - It accepts the IV and the encrypted data as inputs.
      - The IV is converted from a hexadecimal string to a buffer format.
      - A deciphering object is created using the same AES-256-CBC algorithm, the original key, and the provided IV.
      - The encrypted data is decrypted back into its original plaintext form.

   c. **Error Handling**: The decryption process includes error handling to check for invalid input values, such as incorrect IV lengths. If an error occurs, it logs the error message and throws a new user-friendly error.

3. **Security Considerations**:

   - Always ensure the encryption key is kept secret and secure. It should not be hard-coded in the source code.
   - The IV should be unique for each encryption operation to maintain the confidentiality of the data.
   - It is advisable to use additional security measures and best practices when handling sensitive information, such as secure storage solutions for encryption keys.

By using this encryption and decryption process, the application ensures that sensitive data remains protected against unauthorized access, maintaining data confidentiality and integrity.
