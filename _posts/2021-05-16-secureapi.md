---
title: Secure api
date: 2020-05-16
excerpt: "'Secure api' was a challenge in the Web category of dctf 2021"
classes: wide
categories: dctf2021
tags:
  - dctf2021
  - web
  - api
  - jwt
  - johntheripper
  - burpsuite
---

![img](/assets/images/ctf/dctf2021-secureapi/0.png)

We get an error when browsing the site

`{"Error":"Authorization header not found! Try to login with guest credentials."}`

Navigating to `/login` we get another error, this time it's `Method Not Allowed`

Captured the request in **BurpSuite**, changed the request method from **GET** to **POST** and passed in some "guest" credentials


![img](/assets/images/ctf/dctf2021-secureapi/1.png)

The server sends back a **JSON Web Token**. 

```
{"Token":"Bearer eyJ0eXAiOiJKV1QiLCJhbGciOiJIUzUxMiJ9.eyJ1c2VybmFtZSI6Imd1ZXN0IiwiZXhwIjoxNjIxMDI4MzY2fQ.xqKZlUUHQRTRylg4-EtplinoqbCUpERoVdwXDUur0VHLeeAz1v5IOuekeDvsr3JczO4h6bsH2mN4-MWd9u4jOQ"}

```

Passing that in our headers with a **GET** request to the webroot `/`


![img](/assets/images/ctf/dctf2021-secureapi/2.png)

We get this response back

```
{"Message":"Hi, guest! You are not admin, I have no secret for you."}

```

We need to forge the **JWT**. Unfortunately it's not vulnerable to the **Alg None Attack**, so we need to crack the secret key. **John the Ripper** will do that for us.


`john jwt.txt --wordlist=/rockyou.txt --format=HMAC-SHA512`



![img](/assets/images/ctf/dctf2021-secureapi/3.png)

Now that we know the key, we can forge the token. I'm using a **BurpSuite** extension called **JSON Web Tokens**


![img](/assets/images/ctf/dctf2021-secureapi/4.png)

Change the **"username"** field to **"admin"**, click **Recalculate Signature** and pop the secret key in that john just found for us.

Send it off and get the flag!


![img](/assets/images/ctf/dctf2021-secureapi/5.png)
