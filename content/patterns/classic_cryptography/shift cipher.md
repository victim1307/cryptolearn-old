+++
title = "Shift Cipher"
weight = 1
+++

A shift cipher, also known as a Caesar cipher, is a simple encryption technique that replaces each letter of a plaintext message with a letter a fixed number of positions down the alphabet. For example, if the shift value is 3, the letter 'A' would be replaced by 'D', 'B' would be replaced by 'E', and so on.

The shift value is also known as the key, and it determines the encryption and decryption process. The same key is used for both encryption and decryption. The encryption process is simply a shift to the right, and the decryption process is a shift to the left, using the same key value.


#### The formula for a shift cipher encryption is as follows:
| C ≡ (P + K) mod 26 |
|--------------------|

* where:
    - C = the ciphertext (the encrypted message)
    - P = the plaintext (the original message)
    - K = the shift value (the key)
    - mod 26 = the modulo operation that brings the result of the addition within the range of 0 to 25, corresponding to the 26 letters of the alphabet.

#### The formula for a shift cipher decryption is as follows:

| P ≡ (C - K + 26) mod 26 |
|-------------------------|

* where:
    - P = the plaintext (the original message)
    - C = the ciphertext (the encrypted message)
    - K = the shift value (the key)
    - mod 26 = the modulo operation that brings the result of the subtraction within the range of 0 to 25, corresponding to the 26 letters of the alphabet.

### Code

{{<code>}}

def shift_cipher_encryption(plaintext, key):
    # create an empty list to store the ciphertext
    ciphertext = []
    for letter in plaintext:
        # only encrypt letters, not spaces or other characters
        if letter.isalpha():
            # shift the letter by the key value
            shifted_letter = chr((ord(letter) - ord('A') + key) % 26 + ord('A'))
            ciphertext.append(shifted_letter)
        else:
            ciphertext.append(letter)
    return ''.join(ciphertext)

def shift_cipher_decryption(ciphertext, key):
    # create an empty list to store the plaintext
    plaintext = []
    for letter in ciphertext:
        # only decrypt letters, not spaces or other characters
        if letter.isalpha():
            # shift the letter by the negative of the key value
            shifted_letter = chr((ord(letter) - ord('A') - key + 26) % 26 + ord('A'))
            plaintext.append(shifted_letter)
        else:
            plaintext.append(letter)
    return ''.join(plaintext)

# example usage
plaintext = "HELLO WORLD"
key = 3
ciphertext = shift_cipher_encryption(plaintext, key)
print("Ciphertext:", ciphertext)
decrypted_text = shift_cipher_decryption(ciphertext, key)
print("Decrypted text:", decrypted_text)
{{</code>}}
