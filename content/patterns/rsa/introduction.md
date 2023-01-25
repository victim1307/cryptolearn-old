+++
title = "Introduction"
weight = 1
+++

RSA is a widely-used public-key encryption system that is based on the mathematical properties of large prime numbers. It was one of the first practical public-key cryptosystems and is widely used for secure data transmission.

The RSA encryption process consists of two parts: key generation and encryption/decryption.

Key Generation:

+ Select two large prime numbers, p and q.
+ Compute n = p*q. n is used as the modulus for both the public and private keys.
+ Compute the totient of n, φ(n) = (p-1)*(q-1).
+ Select a public exponent e, such that 1 < e < φ(n) and e is coprime to φ(n).
+ Compute the private exponent d, such that d*e = 1 mod φ(n).

Encryption/Decryption:

+ For encryption, the plaintext message is represented as a number m. The ciphertext c is computed as c = m^e mod n.
+ For decryption, the ciphertext c is input and the plaintext message m is computed as m = c^d mod n.

{{<code>}}
from math import gcd
from random import randrange

def generate_keypair(p, q):
    if not (is_prime(p) and is_prime(q)):
        raise ValueError('Both numbers must be prime.')
    elif p == q:
        raise ValueError('p and q cannot be equal')
    n = p * q
    phi = (p-1) * (q-1)
    e = randrange(1, phi)
    g = gcd(e, phi)
    while g != 1:
        e = randrange(1, phi)
        g = gcd(e, phi)
    d = multiplicative_inverse(e, phi)
    return ((e, n), (d, n))

def encrypt(pk, plaintext):
    key, n = pk
    cipher = [(ord(char) ** key) % n for char in plaintext]
    return cipher

def decrypt(pk, ciphertext):
    key, n = pk
    plain = [chr((char ** key) % n) for char in ciphertext]
    return ''.join(plain)
{{</code>}}
