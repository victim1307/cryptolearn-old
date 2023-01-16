+++
title = "Atbash Cipher"
weight = 3
+++

The Atbash Cipher is a simple form of monoalphabetic substitution cipher that uses the reverse of the alphabet as the key.

To encrypt a message, the first step is to reverse the alphabet. This can be done by writing down the alphabet, A-Z or a-z, in the usual order and then writing it down again in reverse order. Then, for each letter in the plaintext message, the corresponding letter in the reversed alphabet is used to encrypt it.

For example, to encrypt the letter “A”, the letter “Z” would be used. To encrypt the letter “B”, the letter “Y” would be used, and so on. The encryption process is done letter by letter in this way, and the resulting encrypted message is the ciphertext.

The decryption process is similar, it's just the reverse of the encryption process, the decryption key is the original alphabet.

Atbash Cipher is a very simple encryption method, it's easy to implement and understand, but it is easily broken by frequency analysis. It's not suitable for use in modern encryption scenarios.

#### The Atbash Cipher encryption process is as follows:

- The first step is to create a reversed alphabet, for example, if we are using the English alphabet, it would be “ZYXWVUTSRQPONMLKJIHGFEDCBA”
- The plaintext message is then converted letter by letter into the corresponding letter in the reversed alphabet.
- The resulting letters form the ciphertext message.

For example, if the plaintext message is “HELLO” and the reversed alphabet is “ZYXWVUTSRQPONMLKJIHGFEDCBA”, the ciphertext message would be “SVOOL”.

#### The Atbash Cipher decryption process is as follows:

- The first step is to use the original alphabet.
- The ciphertext message is then converted letter by letter into the corresponding letter in the original alphabet.
- The resulting letters form the plaintext message.

For example, if the ciphertext message is “SVOOL” and the original alphabet is “ABCDEFGHIJKLMNOPQRSTUVWXYZ”, the plaintext message would be “HELLO”.

It's important to note that this method can be applied to different alphabets and languages, it's just reversing the order of the letters in the alphabet.

### Code

{{<code>}}
def atbash_cipher_encryption(plaintext):
    alphabet = 'ABCDEFGHIJKLMNOPQRSTUVWXYZ'
    reversed_alphabet = alphabet[::-1]
    ciphertext = []
    for letter in plaintext:
        if letter.isalpha():
            index = alphabet.index(letter.upper())
            ciphertext.append(reversed_alphabet[index])
        else:
            ciphertext.append(letter)
    return ''.join(ciphertext)

def atbash_cipher_decryption(ciphertext):
    alphabet = 'ABCDEFGHIJKLMNOPQRSTUVWXYZ'
    reversed_alphabet = alphabet[::-1]
    plaintext = []
    for letter in ciphertext:
        if letter.isalpha():
            index = reversed_alphabet.index(letter.upper())
            plaintext.append(alphabet[index])
        else:
            plaintext.append(letter)
    return ''.join(plaintext)
{{</code>}}