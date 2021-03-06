---
title: Template Shack
date: 2020-12-29
excerpt: "'Template Shack' was a challenge in the Web category of Hacktivitycon"
classes: wide
categories: Hacktivitycon2020
tags:
  - hacktivitycon
  - SSTI
  - RCE
  - web
  - jwt
---

![img](/assets/images/ctf/hacktivitycon-web-templateshack/0.png)


![img](/assets/images/ctf/hacktivitycon-web-templateshack/1.png)


Nothing out of place. Checking the cookies we see what looks to be a JSON Web Token



![img](/assets/images/ctf/hacktivitycon-web-templateshack/2.png)


[jwt.io](http://jwt.io) confirms that it's a JWT and it's using HS256 as the hashing algorithm. Let's see if we can forge our own by cracking this one.



![img](/assets/images/ctf/hacktivitycon-web-templateshack/3.png)


Using jwt-tool to crack the key



![img](/assets/images/ctf/hacktivitycon-web-templateshack/4.png)


Time to forge our own admin JWT:



![img](/assets/images/ctf/hacktivitycon-web-templateshack/5.png)


By changing the cookie value to our new JWT, we've accessed the admin account



![img](/assets/images/ctf/hacktivitycon-web-templateshack/6.png)


Nothing seems to work here, and the only two options that do work kick back a 404.



![img](/assets/images/ctf/hacktivitycon-web-templateshack/7.png)


Interesting. The URL that's causing the error seems to be reflected on the page. Seems like we can control it.



Since the name of the challenge is 'Template Shack', let's jump right into template injection



![img](/assets/images/ctf/hacktivitycon-web-templateshack/new0.png)



![img](/assets/images/ctf/hacktivitycon-web-templateshack/8.png)


Template injection is a go!



Starting with



![img](/assets/images/ctf/hacktivitycon-web-templateshack/new1.png)



we can look for the `'subprocess.Popen'` class



![img](/assets/images/ctf/hacktivitycon-web-templateshack/9.png)


we need it's exact index in the list. Let's use slicing to find it:



![img](/assets/images/ctf/hacktivitycon-web-templateshack/new2.png)



By continuously slicing higher indicies, we can track down exactly where `subprocess.Popen` is



![img](/assets/images/ctf/hacktivitycon-web-templateshack/new3.png)



![img](/assets/images/ctf/hacktivitycon-web-templateshack/10.png)


Now that it's at the top of the list, we know it's at 405



Payload:



![img](/assets/images/ctf/hacktivitycon-web-templateshack/new4.png)



Full url:



![img](/assets/images/ctf/hacktivitycon-web-templateshack/new5.png)



![img](/assets/images/ctf/hacktivitycon-web-templateshack/11.png)
