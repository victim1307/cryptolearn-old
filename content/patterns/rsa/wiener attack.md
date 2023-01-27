+++
title = "Wiener Attack"
weight = 3
+++
The Wiener attack is a method for attacking RSA encryption when the private exponent (d) is small relative to the modulus (n). This method is named after mathematician David Wiener, who first described it in a 1990 paper.

The Wiener attack takes advantage of the fact that the private exponent (d) is typically much smaller than the modulus (n) in RSA encryption. If the private exponent (d) is small enough, it is possible to calculate the private key using the relationship between the private exponent (d) and the public exponent (e) in RSA. The relationship is d*e = 1 (mod φ(n)), where φ(n) is the Euler's totient function of n.

The Wiener attack consists of finding the continued fraction representation of e/n and then using this information to obtain the private key. The process of finding the continued fraction representation of e/n is done by applying the Euclidean algorithm to e and n. Once the continued fraction representation is found, the attack is carried out by computing the convergents of the continued fraction and checking them against the private exponent (d).

The Wiener attack is only possible when the private exponent (d) is small enough, which typically occurs when the public exponent (e) is chosen to be a small number, such as 3 or 65537. In practice, it's recommended to use large public exponents, like 65537, which make Wiener attack infeasible.

It's important to note that the Wiener attack has been largely obsoleted by more powerful methods for attacking RSA encryption, such as the Franklin-Reiter related message attack and the Boneh-Durfee attack, which can be used to recover the private key even when the private exponent is not small relative to the modulus.

{{<code>}}  
from sage.all import ZZ
from sage.all import continued_fraction

def attack(N, e):
    """
    Recovers the prime factors of a modulus and the private exponent if the private exponent is too small.
    :param N: the modulus
    :param e: the public exponent
    :return: a tuple containing the prime factors and the private exponent, or None if the private exponent was not found
    """
    convergents = continued_fraction(ZZ(e) / ZZ(N)).convergents()
    for c in convergents:
        k = c.numerator()
        d = c.denominator()
        if pow(pow(2, e, N), d, N) != 2:
            continue

        phi = (e * d - 1) // k
        factors = known_phi.factorize(N, phi)
        if factors:
            return *factors, int(d)

{{</code>}}