+++
title = "Introduction"
weight = 1
+++
Stream ciphers and block ciphers are two common types of symmetric encryption algorithms.

A stream cipher encrypts plaintext one bit or byte at a time, while a block cipher encrypts plaintext in fixed-size blocks, typically 128 or 256 bits at a time.

Stream ciphers are used in real-time applications where data is transmitted continuously, such as in wireless communications or streaming audio and video. They are efficient in terms of computation and memory usage and can encrypt data quickly and securely. Examples of stream ciphers include A5/1 and RC4.

Block ciphers, on the other hand, are used to encrypt large amounts of data, such as files or entire disk drives. They are more secure than stream ciphers but require more computation and memory resources. Examples of block ciphers include AES and DES.

In both cases, the encryption process is performed using a secret key, and the decryption process is performed using the same key. This ensures that only authorized parties can access the encrypted data.

It's worth noting that both block ciphers and stream ciphers can be used in various modes of operation, like Electronic Codebook (ECB), Cipher Block Chaining (CBC), Cipher Feedback (CFB), Output Feedback (OFB) and Counter (CTR) mode, each one of them has its own security and practical properties.