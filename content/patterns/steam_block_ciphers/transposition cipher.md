+++
title = "Transposition ciphers"
weight = 4
+++

Transposition ciphers are a type of encryption technique that rearrange the positions of the letters in the plaintext to produce the ciphertext. The plaintext is rearranged according to a specific rule or method, such as a regular pattern or a secret key. The process of encryption is reversible, meaning that the original plaintext can be obtained by rearranging the ciphertext using the same rule or method.

There are several types of transposition ciphers, such as:

Columnar Transposition: This cipher rearranges the letters of the plaintext by writing them in a grid and then reading the columns in a specific order.

Rail Fence: This cipher rearranges the letters of the plaintext by writing them in a zigzag pattern along a set number of "rails" and then reading the letters off in a specific order.

Route Cipher: This cipher rearranges the letters of the plaintext by writing them in a grid and then reading the letters off in a specific route, such as a snake-like pattern.

Book Cipher: This cipher rearranges the letters of the plaintext by assigning each letter a number and then using a book or other prearranged text to look up the corresponding ciphertext letter.

It's important to note that transposition ciphers are not considered very secure encryption method and can be easily broken by frequency analysis and other methods. They are mainly used to provide an additional layer of security on top of another encryption method.

{{<code>}}

def columnar_transposition_encryption(plaintext:str, key:str):
    ciphertext = ""
    grid = []
    for i in range(len(plaintext)):
        grid.append(plaintext[i])
    for i in range(len(key)):
        ciphertext += grid[i::len(key)]
    return ciphertext

def columnar_transposition_decryption(ciphertext:str, key:str):
    plaintext = ""
    grid = []
    for i in range(len(ciphertext)):
        grid.append(ciphertext[i])
    for i in range(len(key)):
        plaintext += grid[i::len(key)]
    return plaintext

{{</code>}}
