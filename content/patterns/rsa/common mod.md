+++
title = "Common Modulus Attack"
weight = 2
+++
A common modulus attack on RSA is a type of cryptographic attack that takes advantage of the properties of RSA encryption when the same modulus is used for multiple encryptions.

In RSA, encryption is performed by raising the plaintext message to the power of the public exponent (e) and taking the remainder when divided by the modulus (n). Similarly, decryption is performed by raising the ciphertext to the power of the private exponent (d) and taking the remainder when divided by the modulus (n).

In a common modulus attack, an attacker intercepts multiple ciphertexts that have been encrypted using the same modulus (n), but with different public exponents (e1, e2, ..., en). The attacker can then use mathematical techniques to recover the plaintext message, even if the private exponent (d) is not known.

One way to perform a common modulus attack is to use the Chinese Remainder Theorem (CRT) to combine the equations of multiple ciphertexts, allowing the attacker to solve for the plaintext. Another way is to use the Euclidean algorithm to calculate the greatest common divisor of the multiple public exponents (e1, e2, ..., en) and the modulus (n) to obtain the private exponent (d) and then use it to decrypt the ciphertexts.

{{<code>}}
from sage.all import xgcd


def attack(n, e1, c1, e2, c2):
    """
    Recovers the plaintext from two ciphertexts, encrypted using the same modulus and different public exponents.
    :param n: the common modulus
    :param e1: the first public exponent
    :param c1: the ciphertext of the first encryption
    :param e2: the second public exponent
    :param c2: the ciphertext of the second encryption
    :return: the plaintext
    """
    _, u, v = xgcd(e1, e2)
    p1 = pow(c1, u, n) if u > 0 else pow(pow(c1, -1, n), -u, n)
    p2 = pow(c2, v, n) if v > 0 else pow(pow(c2, -1, n), -v, n)
    return int(p1 * p2) % n
{{</code>}}