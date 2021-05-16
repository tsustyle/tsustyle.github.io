---
title: Behind the Scenes
date: 2020-05-16
excerpt: "'Behind the Scenes' was a challenge in the Misc category of dctf 2021"
classes: wide
categories: dctf2021
tags:
  - dctf2021
  - misc
  - depix
---

![img](/assets/images/ctf/dctf2021-behindthescenes/0.png)

We're given an image with a pixelated password entry on a notepad


![img](/assets/images/ctf/dctf2021-behindthescenes/1.png)

We're going to use a tool called `Depix`

https://github.com/beurtschipper/Depix

Using image editing software (I used gimp) we need to grab **only** the pixelated portion, and it needs to line up perfectly


![img](/assets/images/ctf/dctf2021-behindthescenes/2.png)

Send that to **Depix**

`python3 depix.py -p ~/newcropped.png -s images/searchimages/debruinseq_notepad_Windows10_close.png
`

gives us this as the output


![img](/assets/images/ctf/dctf2021-behindthescenes/3.png)

`dctf{GotAnyMorePixels}`

