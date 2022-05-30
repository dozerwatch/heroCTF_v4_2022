# Poly321

### Category
Crypto

### Description
An unskilled mathematician has created an encryption function. Can you decrypt the message ?

### File
- [encrypt.py](https://github.com/HeroCTF/HeroCTF_v4/blob/main/Crypto/Poly321/encrypt.py)

``` python
#!/usr/bin/env python3


FLAG = "****************************"

enc = []
for c in FLAG:
    v = ord(c)

    enc.append(
        v + pow(v, 2) + pow(v, 3)
    )

print(enc)

"""
$ python3 encrypt.py
[378504, 1040603, 1494654, 1380063, 1876119, 1574468, 1135784, 1168755, 1534215, 866495, 1168755, 1534215, 866495, 1657074, 1040603, 1494654, 1786323, 866495, 1699439, 1040603, 922179, 1236599, 866495, 1040603, 1343210, 980199, 1494654, 1786323, 1417584, 1574468, 1168755, 1380063, 1343210, 866495, 188499, 127550, 178808, 135303, 151739, 127550, 112944, 178808, 1968875]
"""
```

### Solution

We see that ```encrypt.py``` loops over the ```FLAG``` and ```ord``` every letter. Then it performs the following operation on it.

$$ c = v + v^2 + v^3 $$

The variable ```c``` is the resulting answer, which is given to us in the commented out section. We need to find what value ```v``` is. Isolating ```v``` seems to be a very difficult task, so I decided to brute force it instead. Since commputers are quick and knowing that the flag will be in ASCII format, a range of 200 is more than enough.

``` python
enc = [378504, 1040603, 1494654, 1380063, 1876119, 1574468, 1135784, 1168755, 1534215, 866495, 1168755, 1534215, 866495, 1657074, 1040603, 1494654, 1786323, 866495, 1699439, 1040603, 922179, 1236599, 866495, 1040603, 1343210, 980199, 1494654, 1786323, 1417584, 1574468, 1168755, 1380063, 1343210, 866495, 188499, 127550, 178808, 135303, 151739, 127550, 112944, 178808, 1968875]

ans = []

for num in enc:
    for i in range(200):
        if (i+pow(i,2)+pow(i,3) == num):
            ans.append(i)
            
for n in ans:
    print(chr(n),end='')
```

### Flag

```Hero{this_is_very_weak_encryption_92835208}```






