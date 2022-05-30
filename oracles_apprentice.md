# The oracle's apprentice

### Category

Crypto

### Description

Looks like the oracle took a nice long holiday and her apprentice had to cover for her. She's new to the job so if she forgets anything... you'll just have to deal with it. Good luck !

### File

- [chall.py](https://github.com/HeroCTF/HeroCTF_v4/blob/main/Crypto/Oracles_apprentice/chall.py)

``` python
#!/usr/bin/env python3
from Crypto.Util.number import getStrongPrime, bytes_to_long
import random

FLAG = open('flag.txt','rb').read()

encrypt = lambda m: pow(m, e, n)
decrypt = lambda c: pow(c, d, n)

e = random.randrange(3, 65537, 2)
p = getStrongPrime(1024, e=e)
q = getStrongPrime(1024, e=e)

n = p * q
φ = (p-1) * (q-1)

d = pow(e, -1, φ)

c = encrypt(bytes_to_long(FLAG))

#print(f"{n=}")
#print(f"{e=}")
print(f"{c=}")

for _ in range(3):
     t = int(input("c="))
     print(decrypt(t)) if c != t else None
```

## Solution

The trick here is that unpadded RSA is a homomorphic encryption, which means that we can do operations on the encrypted data. So we have the following:

```
c1 * c2 = encrypt(m1 * m2)
```

But what if c1 and c2 are the same? Then $c^2 = $ encrypt $(m^2)$ where $c$ is the given ciphertext from the program and $m$ is the flag. So all we have to do is to square the ciphertext and send that as the input. Then we square root the output.

``` python
from Crypto.Util.number import long_to_bytes

#m2 = ... [this is the output from our input]

import gmpy2

m, b = gmpy2.iroot(m2,2) # square roots m2

print(long_to_bytes(m))
```

### Flag

```Hero{m4ybe_le4ving_the_1nt3rn_run_th3_plac3_wasnt_a_g00d_id3a}```
