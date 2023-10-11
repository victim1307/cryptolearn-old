+++
title = "Introduction"
weight = 1
+++

The Diffie-Hellman key exchange is the method of safely developing and exchanging keys over an insecure channel. It allows two parties to establish a shared secret key over an unsecured communication channel. Unlike RSA, which is primarily used for encryption, Diffie-Hellman is focused on secure key exchange.

Working:

+ Let's say, two parties, Alice and Bob agree on two large prime numbers, p and g, and a public key exchange algorithm.
+ Alice chooses a secret integer, a, and computes A = g^a mod p. She sends A to Bob.
+ Bob chooses a secret integer, b, and computes B = g^b mod p. He sends B to Alice.
+ Alice computes s = B^a mod p. Bob computes s = A^b mod p.
+ Alice and Bob now both have the shared secret key s, which they can use to establish a secure communication channel.

The security of the Diffie-Hellman key exchange relies on the fact that it is computationally infeasible for an attacker to determine the shared secret keys from the public values of p, g, A, and B. This allows Alice and Bob to exchange the key securely, even over an insecure channel.

The most interesting part of the Diffie-Hellman key exchange is that both parties end up with the same result, without ever needing to send the entirety of the common secret across the communication channel.

{{<code>}}

import random

p = 29              # Shared prime number and base (these should be agreed upon in advance)
g = 7

alice_private = random.randint(1, p - 1)            # Alice's private key

bob_private = random.randint(1, p - 1)            # Bob's private key

alice_public = (g ** alice_private) % p                 # Compute public keys
bob_public = (g ** bob_private) % p

# Alice and Bob exchanges public keys with each other

alice_shared_secret = (bob_public ** alice_private) % p           # Alice and Bob now compute the shared secret
bob_shared_secret = (alice_public ** bob_private) % p

# The shared secrets should be the same
print("Shared Secret (Alice):", alice_shared_secret)
print("Shared Secret (Bob):", bob_shared_secret)
{{</code>}}