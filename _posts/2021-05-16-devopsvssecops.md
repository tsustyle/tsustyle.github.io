---
title: DevOps vs SecOps
date: 2020-05-16
excerpt: "'DevOps vs SecOps' was a challenge in the Web category of dctf 2021"
classes: wide
categories: dctf2021
tags:
  - dctf2021
  - web
  - github
  - osint
---

![img](/assets/images/ctf/dctf2021-devopsvssecops/0.png)

Figured it was something OSINT-y, so turned to google and github

https://github.com/DragonSecSI/DCTF1-chall-devops-vs-secops

There are two branches. One of them reference another repo `- name: Checkout .github`

`setup.py` in the `.github` repo

```
if __name__ == "__main__":
    init()
    print("dctf{H3ll0_fr0m_1T_guy}")
    os.system(f"ctf challenge sync challenge.yml ;ctf challenge install challenge.yml ")
```
