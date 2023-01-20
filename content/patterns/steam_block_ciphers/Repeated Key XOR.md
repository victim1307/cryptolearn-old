+++
title = "Repeated Key XOR"
weight = 3
+++

Repeated Key XOR is a type of encryption that uses the XOR operation to encrypt plaintext by repeatedly applying a secret key to it. In this method, the key is repeated as many times as necessary to match the length of the plaintext. The encryption process works by taking each plaintext byte and the corresponding byte of the key, and applying the XOR operation between them. The result is the ciphertext.

Decryption is the inverse process of encryption, it takes the ciphertext and the same key used for encryption and applies the XOR operation between them, which results in the original plaintext.

{{<code>}}
def repeated_key_xor_encryption(plaintext:str, key:str):
    ciphertext = ""
    for i in range(len(plaintext)):
        ciphertext += chr(ord(plaintext[i]) ^ ord(key[i % len(key)]))
    return ciphertext

def repeated_key_xor_decryption(ciphertext:str, key:str):
    plaintext = ""
    for i in range(len(ciphertext)):
        plaintext += chr(ord(ciphertext[i]) ^ ord(key[i % len(key)]))
    return plaintext
{{</code>}}