---
title: Phriedman Systems
date: 2020-05-08
excerpt: "'Phriedman Systems' was a challenge in the Fwn category of DawgCTF 2021"
classes: wide
categories: dawgctf2021
tags:
  - dawgctf2021
  - fwn
  - phone
  - recon
  - web
---


![img](/assets/images/ctf/dawgctf2021-phriedmansystems/0.png)

We need to log in with the CEO's account

```
"Ever since I started my first business selling computer parts in my hometown, I've been personally committed to quality service, professionalism, ethical business practices, and extreme mission efficacy."

~ Our CEO, Conrad Smith (pictured right)

Few know that Phriedman Systems began as a mere ceilometer manufacturer, branching off from our CEO's first business. Over time we diversified to obtain our vast portfolio of today's products and services. We moved down to the DMV in 2014 to better facilitate service for customers in the region. To hear all about our exciting corporate story, feel free to contact us and ask about company info. 
```

```
Conrad Smith - CEO
Hi! I'm the CEO of Phriedman. I'm very proud of my company and the important work we do every day.
Office 30 
```

`https://phriedmansystems.onrender.com/login.html`

Found the login



![img](/assets/images/ctf/dawgctf2021-phriedmansystems/1.png)


![img](/assets/images/ctf/dawgctf2021-phriedmansystems/2.png)

`csmith` exists, probably the CEO username

Dug around in the source code, but the login function is secure. Going back to the hints it says that it's more of a recon challenge. The phone number works!

Press 1: Company Info. CEO tells us that he's from Albany.
Press 4: IT Department
Press 3: Automated Assistance
Pess 2: Password Recovery
Using the keypad, input `csmith`
Asks us to provide the answer to the security question.
CEO Security Question: Name of hometown?
Using the keypad, input `Albany`

It then reads us the password:

`monkey_alpaca_excellent_button_7435`



![img](/assets/images/ctf/dawgctf2021-phriedmansystems/3.png)
