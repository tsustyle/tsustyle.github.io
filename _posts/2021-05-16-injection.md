---
title: Injection
date: 2020-05-16
excerpt: "'Injection' was a challenge in the Web category of dctf 2021"
classes: wide
categories: dctf2021
tags:
  - dctf2021
  - web
  - ssti
  - jinja2
---


![img](/assets/images/ctf/dctf2021-injection/0.png)


![img](/assets/images/ctf/dctf2021-injection/1.png)

Giving it any input sends us to a page that says

```
Oops! Page login doesn't exist :(
```

Testing the url, I noticed that it's getting reflected

`/<u>memes</u>`


![img](/assets/images/ctf/dctf2021-injection/2.png)

Using the title of the challenge as a hint, I tried **Server Side Template Injection**

`/{{7*7}}`

Kicks back

```
Oops! Page 49 doesn't exist :(
```

Going through the normal tests, I landed on `{{7*'7'}}` which kicked back `7777777` and confirms that it's **Jinja2**.

Reading: https://github.com/swisskyrepo/PayloadsAllTheThings/tree/master/Server%20Side%20Template%20Injection

Using this payload


![img](/assets/images/ctf/dctf2021-injection/3.png)

Grants us RCE. *`(${IFS} acts as a space character)`*

Sending the request in **BurpSuite**, we can see the contents of our current directory


![img](/assets/images/ctf/dctf2021-injection/4.png)

Inside the `lib/` directory we have an odd script


![img](/assets/images/ctf/dctf2021-injection/5.png)

Catting it out with `.popen('cat${IFS}lib/security.py')`


![img](/assets/images/ctf/dctf2021-injection/6.png)

Let's clean it up

```
valid_password = 'QfsFjdz81cx8Fd1Bnbx8lczMXdfxGb0snZ0NGZ'
return base64.b64encode(password.encode('ascii')).decode('ascii')[::-1].lstrip('=') == valid_password
```

Basically it's going to take in a value, base64 encode it, reverse it and strip away any padding ('=' characters)

Knowing that, we can reverse the `valid_password` variable and add padding to it as needed to get a "valid password"

This is the quick script I used

```
import base64
 
print(base64.b64decode('==QfsFjdz81cx8Fd1Bnbx8lczMXdfxGb0snZ0NGZ'[::-1]))
```


![img](/assets/images/ctf/dctf2021-injection/7.png)

Oh, it's the flag!
