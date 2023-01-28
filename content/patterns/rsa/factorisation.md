+++
title = "Factorisation"
weight = 4
+++
### Fermat's Factorisation Method
Fermat's factorization is an algorithm for factoring integers that is based on Fermat's Little Theorem. The theorem states that if p is a prime number, then for any integer a, the number a^p - a is an integer multiple of p. The algorithm for factoring an integer N is to find two integers a and b such that a^2 - Nb^2 = 1. If such integers are found, then N is the product of the two factors a+b and a-b. The algorithm is based on the idea that if N is composite, then it is possible to find such integers a and b by trying different values of a and using the equation to calculate b. However, this method is not always efficient and has been largely superseded by more efficient algorithms such as the General Number Field Sieve.

{{<code>}}
from math import isqrt

def is_square(x):
    """
    Returns the square root of x if x is a perfect square, or None otherwise.
    :param x: x
    :return: the square root of x or None
    """
    y = isqrt(x)
    return y if y ** 2 == x else None

def factorize(N):
    """
    Recovers the prime factors from a modulus using Fermat's factorization method.
    :param N: the modulus
    :return: a tuple containing the prime factors, or None if the factors were not found
    """
    a = isqrt(N)
    b = a * a - N
    while b < 0 or not is_square(b):
        a += 1
        b = a * a - N

    p = a - isqrt(b)
    q = N // p
    if p * q == N:
        return p, q

{{</code>}}