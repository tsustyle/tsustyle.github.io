---
title: This one really is basic
date: 2020-05-16
excerpt: "'This one really is basic' was a challenge in the Misc category of dctf 2021"
classes: wide
categories: dctf2021
tags:
  - dctf2021
  - base64
  - python
  - crypto
---

![img](/assets/images/ctf/dctf2021-thisonereallyisbasic/0.png)

`Base64` `42` times

```
import base64

with open('cipher.txt', 'r') as f:
    data = f.read()

for i in range(42):
    data = base64.b64decode(data)

print(data)
```
