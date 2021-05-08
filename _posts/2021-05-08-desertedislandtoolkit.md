---
title: Deserted Island Toolkit
date: 2020-05-08
excerpt: "'Deserted Island Toolkit' was a challenge in the Audio/Radio category of DawgCTF 2021"
classes: wide
categories: dawgctf2021
tags:
  - dawgctf2021
  - audio
  - radio
  - morse
---


![img](/assets/images/ctf/dawgctf2021-desertedislandtoolkit/0.png)

We're given an **iso** file, mounting it reveals a **cdda** file.

https://wiki.archlinux.org/title/Rip_Audio_CDs

using **lame** to turn the **cdda** into an **mp3**

`lame -V0 is/dawgTunes.cdda memes.mp3`

The audio file plays a series of morse code characters, decoding it gives us

`S0SISNOTTHEAN5W3R`
