+++
title = "Hastad's Broadcast Attack"
weight = 2
+++

## Hastad's Broadcast Attack on unpadded messages
Consider a scenario where Alice transmits an unpadded message (M) to k people labeled P1,P2,...,Pk. Each recipient has an identical small public key exponent (e) and distinct moduli (N) for every ith individual (Ni,e). Here the vulnerability arises when the number of recipients k is greater than or equal to e (k>=e). Once this happens the security of message M is compromised and it can be recovered through application of Chinese Remainder Theorem.

To illustrate this attack, let's consider a example where Alice sends a message M to 3 three different people using the same public key exponent e = 3. Let the ciphertext received by ith receiver be Ci where Ci = M3 mod Ni. We have to assume that gcd(Ni, Nj) == 1 where i != j.

Now we can write :
$$
M^3 = C_1 \mod N_1 \\
M^3 = C_2 \mod N_2 \\
M^3 = C_3 \mod N_3 \\
$$
Thus we can get the following by solving using Chinese Remainder Theorem:
$$
M^3 = \sum_{i=1}^{3} C_i b_i b'_i \pmod{N}
$$
where *bi = N/Ni, bi' = bi-1 mod Ni and N = N1 N2 N3*. Since we know that M < Ni (If our message M is larger than the modulus N, then we won't get the exact message when we decrypt the ciphertext, we will get an equivalent message instead, which is not favourable).
Therefore we can write M < N1N2N3. We can easily calculate M now by directly taking the cube root of M3 to get M.

Hastad also showed that applying linear padding to the message M prior to encryption does not protect from this attack.


{{<code>}}
import os
import sys
from math import gcd

path = os.path.dirname(os.path.dirname(os.path.dirname(os.path.realpath(os.path.abspath(__file__)))))
if sys.path[1] != path:
    sys.path.insert(1, path)

from attacks.rsa import low_exponent
from shared.crt import fast_crt


def attack(N, e, c):
    """
    Recovers the plaintext from e ciphertexts, encrypted using different moduli and the same public exponent.
    :param N: the moduli
    :param e: the public exponent
    :param c: the ciphertexts
    :return: the plaintext
    """
    assert e == len(N) == len(c), "The amount of ciphertexts should be equal to e."

    for i in range(len(N)):
        for j in range(len(N)):
            if i != j and gcd(N[i], N[j]) != 1:
                raise ValueError(f"Modulus {i} and {j} share factors, Hastad's attack is impossible.")

    c, _ = fast_crt(c, N)
    return low_exponent.attack(e, c)
{{</code>}}
