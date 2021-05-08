---
title: MDL Considered Harmful
date: 2020-05-08
excerpt: "'MDL Considered Harmful' was a challenge in the Pwn category of DawgCTF 2021"
classes: wide
categories: dawgctf2021
tags:
  - dawgctf2021
  - pwn
  - discord
  - imagemagick
  - imagetragick
---


![img](/assets/images/ctf/dawgctf2021-mdlconsideredharmful/0.png)

using `/help`


![img](/assets/images/ctf/dawgctf2021-mdlconsideredharmful/1.png)

Neat! Let's try


![img](/assets/images/ctf/dawgctf2021-mdlconsideredharmful/2.png)

The bot has other commands. For example, `/credits`


![img](/assets/images/ctf/dawgctf2021-mdlconsideredharmful/3.png)

Alarm bells starting going off in my head immediately upon reading `ImageMagick`

`ImageMagick` is an open-source image processing software suite that, well, has had some issues in the past. There are quite a few exploits we can look at, but the main one that we're interested in for this case is

`CVE-2016-3717`


![img](/assets/images/ctf/dawgctf2021-mdlconsideredharmful/4.png)

By passing in `@/opt/flag.txt` we're able to read the contents of the flag file. This works for any file that you know the location of and have permissions to view


![img](/assets/images/ctf/dawgctf2021-mdlconsideredharmful/5.png)
