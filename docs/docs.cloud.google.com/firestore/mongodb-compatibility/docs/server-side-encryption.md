# Server-side encryption

Firestore with MongoDB compatibility automatically encrypts all data before it is written to disk. There is no setup or configuration required and no need to modify the way you access the service. The data is automatically and transparently decrypted when read by an authorized user.

## Key management

With server-side encryption, you can either let Google manage cryptographic keys on your behalf or use customer-managed encryption keys (CMEK) to manage the keys yourself.

By default, Google manages cryptographic keys on your behalf using the same hardened key management systems that we use for our own encrypted data, including strict key access controls and auditing. Each Firestore with MongoDB compatibility object's data and metadata is [encrypted](https://cloud.google.com/docs/security/encryption/default-encryption) and each encryption key is itself encrypted with a regularly rotated set of master keys.

For information about managing keys yourself, see [CMEK for Firestore with MongoDB compatibility](/firestore/mongodb-compatibility/docs/cmek) .

## Client-side encryption

Server-side encryption can be used in combination with client-side encryption. In client-side encryption, you manage your own encryption keys and encrypt data before writing it to Firestore with MongoDB compatibility. In this case, your data is encrypted twice, once with your keys and once with the server-side keys.

**Warning:** Firestore with MongoDB compatibility does not know if your data has already been encrypted client-side, nor does Firestore with MongoDB compatibility have any knowledge of your client-side encryption keys. If you use client-side encryption, you must securely manage your encryption keys.

To protect your data as it travels over the Internet during read and write operations, we use Transport Layer Security (TLS). For more information about the supported TLS versions, see [Encryption in transit in Google Cloud](https://cloud.google.com/docs/security/encryption-in-transit#user_to_google_front_end_encryption) .

## What's next

For more information about encryption at rest for Firestore with MongoDB compatibility and other Google Cloud products, see [Encryption at Rest in Google Cloud](https://cloud.google.com/docs/security/encryption/default-encryption) .
