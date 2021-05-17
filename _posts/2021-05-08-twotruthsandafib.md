---
title: Two Truths and a Fib
date: 2020-05-08
excerpt: "'Two Truths and a Fib' was a challenge in the Misc category of DawgCTF 2021"
classes: wide
categories: dawgctf2021
tags:
  - dawgctf2021
  - misc
  - python
  - scripting
---


![img](/assets/images/ctf/dawgctf2021-twotruthsandafib/0.png)

```
import math
from pwn import *
import re

# Fib functions pulled from
# https://www.geeksforgeeks.org/python-program-for-how-to-check-if-a-given-number-is-fibonacci-number/

# A utility function that returns true if x is perfect square
def isPerfectSquare(x):
    s = int(math.sqrt(x))
    return s*s == x
  
# Returns true if n is a Fibinacci Number, else false
def isFibonacci(n):
  
    # n is Fibinacci if one of 5*n*n + 4 or 5*n*n - 4 or both
    # is a perferct square
    return isPerfectSquare(5*n*n + 4) or isPerfectSquare(5*n*n - 4)

conn = remote('umbccd.io', 6000)
print(conn.recvuntil('\n\n\n'))

#initial
while True:
    try:
        #main
        numbers = re.findall('[0-9]+', conn.recvuntil(']').decode('utf-8'))
        fibnum = ''
        print(numbers)

        for i in numbers:
            if isFibonacci(int(i)):
                fibnum = i

        conn.sendline(fibnum)
        #end
        conn.recvline()
        print(conn.recvline())
        print(conn.recvline())
    except:
        conn.interactive()
```
