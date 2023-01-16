+++
title = "Shift Cipher"
weight = 1
+++

A shift cipher, also known as a Caesar cipher, is a simple encryption technique that replaces each letter of a plaintext message with a letter a fixed number of positions down the alphabet. For example, if the shift value is 3, the letter 'A' would be replaced by 'D', 'B' would be replaced by 'E', and so on.

The shift value is also known as the key, and it determines the encryption and decryption process. The same key is used for both encryption and decryption. The encryption process is simply a shift to the right, and the decryption process is a shift to the left, using the same key value.



#### The formula for a shift cipher encryption is as follows:
                            C ≡ (P + K) mod 26

* where:
    * C = the ciphertext (the encrypted message)
    * P = the plaintext (the original message)
    * K = the shift value (the key)
    * mod 26 = the modulo operation that brings the result of the addition within the range of 0 to 25, corresponding to the 26 letters of the alphabet.

#### The formula for a shift cipher decryption is as follows:

                            P ≡ (C - K + 26) mod 26

* where:
    * P = the plaintext (the original message)
    * C = the ciphertext (the encrypted message)
    * K = the shift value (the key)
    * mod 26 = the modulo operation that brings the result of the subtraction within the range of 0 to 25, corresponding to the 26 letters of the alphabet.