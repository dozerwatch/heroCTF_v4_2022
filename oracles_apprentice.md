# The oracle's apprentice

### Category

Crypto

### Description

Looks like the oracle took a nice long holiday and her apprentice had to cover for her. She's new to the job so if she forgets anything... you'll just have to deal with it. Good luck !

### File

- [chall.py](https://github.com/HeroCTF/HeroCTF_v4/blob/main/Crypto/Oracles_apprentice/chall.py)

## Solution

The trick here is that unpadded RSA encryptions are homeomorphic, which means that we can do operations on the encrypted data. So we have the following:

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
