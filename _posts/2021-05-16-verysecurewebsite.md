---
title: Very Secure Website
date: 2020-05-16
excerpt: "'Very Secure Website' was a challenge in the Web category of dctf 2021"
classes: wide
categories: dctf2021
tags:
  - dctf2021
  - web
  - php
  - loosecomparison
  - typejuggling
---

![img](/assets/images/ctf/dctf2021-verysecurewebsite/0.png)

The source code is given

Here's a snippet

```
if (hash("tiger128,4", $_GET['username']) != "51c3f5f5d8a8830bc5d8b7ebcb5717df") {
            echo "Invalid username";
        }
        else if (hash("tiger128,4", $_GET['password']) == "0e132798983807237937411964085731") {
```

Googling the username hash we get `admin`

The password check is based on **PHP loose comparison** or **PHP Type Juggling** whichever you prefer. **==** is loose, **===** is strict. I'm going to be honest, I don't know why it works just that it does.

Here's a list of values and hashes that will work:

https://github.com/spaze/hashes/blob/master/tiger128,4.md


`dctf{It's_magic._I_ain't_gotta_explain_shit.}`

Agreed
