+++
title = "Affine Cipher"
weight = 2
+++

An Affine cipher is a type of monoalphabetic substitution cipher, in which each letter in the plaintext is mapped to a unique fixed letter in the ciphertext. This mapping is based on a mathematical function, called the Affine function, that takes two inputs: the letter of the plaintext and two encryption keys, "a" and "b".

#### The encryption function is defined as:
| C = (a*P + b) mod 26 |
|----------------------|

* Where:
    * C = the ciphertext letter (the encrypted letter)
    * P = the plaintext letter (the original letter)
    * a, b = the encryption keys
    * mod 26 = the modulo operation that brings the result of the multiplication and addition within the range of 0 to 25, corresponding to the 26 letters of the alphabet.

To decrypt the ciphertext, the function uses the inverse of the encryption key 'a' and the encryption key 'b' to obtain the plaintext.

#### The decryption function is defined as:
| P = (a^-1 * (C - b)) mod 26 |
|-----------------------------|

* Where:
    * P = the plaintext letter (the original letter)
    * C = the ciphertext letter (the encrypted letter)
    * a^-1 = the modular inverse of a (a^-1 * a = 1 mod 26)
    * b = the encryption key
    * mod 26 = the modulo operation that brings the result of the multiplication and subtraction within the range of 0 to 25, corresponding to the 26 letters of the alphabet.

The encryption and decryption keys "a" and "b" must be chosen such that "a" is relatively prime to 26 (i.e. it has no factors in common with 26) and that the modular inverse of "a" exists.

### Code

{{<code>}}
def affine_cipher_encryption(plaintext, a, b):
    # create an empty list to store the ciphertext
    ciphertext = []
    for letter in plaintext:
        # only encrypt letters, not spaces or other characters
        if letter.isalpha():
            # encrypt the letter using the Affine function
            encrypted_letter = chr(((a * (ord(letter) - ord('A'))) + b) % 26 + ord('A'))
            ciphertext.append(encrypted_letter)
        else:
            ciphertext.append(letter)
    return ''.join(ciphertext)

def affine_cipher_decryption(ciphertext, a, b):
    # calculate the modular inverse of a
    a_inv = inverse_mod(a, 26)
    # create an empty list to store the plaintext
    plaintext = []
    for letter in ciphertext:
        # only decrypt letters, not spaces or other characters
        if letter.isalpha():
            # decrypt the letter using the inverse Affine function
            decrypted_letter = chr((a_inv * ((ord(letter) - ord('A')) - b)) % 26 + ord('A'))
            plaintext.append(decrypted_letter)
        else:
            plaintext.append(letter)
    return ''.join(plaintext)

# example usage
plaintext = "HELLO WORLD"
a = 5
b = 8
ciphertext = affine_cipher_encryption(plaintext, a, b)
print("Ciphertext:", ciphertext)
decrypted_text = affine_cipher_decryption(ciphertext, a, b)
print("Decrypted text:", decrypted_text)
{{</code>}}
