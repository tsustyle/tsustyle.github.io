---
title: Baby's First Modulation
date: 2020-05-08
excerpt: "'Baby's First Modulation' was a challenge in the Audio/Radio category of DawgCTF 2021"
classes: wide
categories: dawgctf2021
tags:
  - dawgctf2021
  - audio
  - radio
---


![img](/assets/images/ctf/dawgctf2021-babysfirstmodulation/0.png)

We're given an **IQ** file. I used **sox** on a Windows machine to convert it to a **.wav** file and then sped it up in audacity. 

sox command:
`./sox.exe -e float -t raw -r 192000 -b 32 -c 2 D:/Downloads/rf1.iq -t wav -e float -b 32 -c 2 -r 192000 memes.wav
`

DawgCTF{listen_in_on_the_waves}
