+++
title = "Single Byte XOR"
weight = 2
+++
Single-Byte XOR, also known as Single Character XOR, is a simple form of XOR encryption that encrypts each byte of the plaintext message using a single byte key. The encryption process is done by applying the XOR operation between the plaintext byte and the key byte.

The decryption process is the same as the encryption process, it's just the reverse of the encryption process, the decryption key is the same key used for encryption.

Here's an example of how you might implement Single-Byte XOR encryption and decryption in Sage:

{{<code>}}
def single_byte_xor_encryption(plaintext, key):
    ciphertext = ""
    for i in range(len(plaintext)):
        ciphertext += chr(ord(plaintext[i]) ^ ord(key[i % len(key)]))
    return ciphertext

def single_byte_xor_decryption(ciphertext, key):
    plaintext = ""
    for i in range(len(ciphertext)):
        plaintext += chr(ord(ciphertext[i]) ^ ord(key[i % len(key)]))
    return plaintext
{{</code>}}

It's important to note that Single-Byte XOR is not considered a secure encryption method and should not be used in real-world scenarios, it can be easily broken by frequency analysis, and other methods.