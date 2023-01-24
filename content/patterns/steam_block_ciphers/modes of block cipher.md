+++
title = "Modes of block cipher"
weight = 5
+++

A block cipher is a type of symmetric key encryption that encrypts data in fixed-size blocks (typically 64 or 128 bits). There are several different modes of encryption that can be used with a block cipher to encrypt data of any size:

Electronic Code Book (ECB) mode: This is the simplest and most basic mode of encryption. Each block of plaintext is independently encrypted with the same key, resulting in a block of ciphertext of the same size. However, ECB mode is vulnerable to certain types of attacks, such as a known-plaintext attack, where an attacker can determine the key by analyzing a large number of ciphertext blocks.

Cipher Block Chaining (CBC) mode: In this mode, a unique initialization vector (IV) is used to encrypt the first block of plaintext. For subsequent blocks of plaintext, the previous block of ciphertext is XORed with the current block of plaintext before encryption. This creates a chain of ciphertext blocks that are dependent on each other, making it more secure than ECB mode.

Cipher Feedback (CFB) mode: This mode is similar to CBC mode, but instead of using the previous block of ciphertext, a block of ciphertext is used to encrypt the next block of plaintext. This creates a similar chain of ciphertext blocks that are dependent on each other, making it more secure than ECB mode.

Output Feedback (OFB) mode: In this mode, a block of ciphertext is used to encrypt the next block of plaintext, but unlike CFB mode, the ciphertext is not fed back into the encryption process. This creates a similar chain of ciphertext blocks that are dependent on each other, making it more secure than ECB mode.

Counter (CTR) mode: This mode uses a counter to encrypt the plaintext. The counter is combined with the key to encrypt each block of plaintext. This mode is similar to OFB mode but the encryption process is slightly more complex. It's considered to be more secure than ECB and other feedback modes.