---
title: THM Challenge
date: 2021-02-11
excerpt: "'THM Challenge' is a WebApp that I wrote to send along with my CV to TryHackMe when they were recruiting Content Engineers"
classes: wide
categories: TryHackMe
tags:
  - thm
  - tsustyle
  - python
  - flask
  - xss
---

![3c514ce4b4bf3eb88c1e193655cf7b08.png](/assets/images/thm/thmchallenge/0.png)

`/robots.txt` has some Disallows

```
User-agent: *
Disallow: /admin
Disallow: /todo
```

Admin is a rabbithole. `todo` actually has some info.

![3c514ce4b4bf3eb88c1e193655cf7b08.png](/assets/images/thm/thmchallenge/1.png)

Looks like there's a new feature that hasn't been sufficiently tested for security holes.

Register an account to get a look at the member's area

![3c514ce4b4bf3eb88c1e193655cf7b08.png](/assets/images/thm/thmchallenge/2.png)

So we can upload a resume or send a request to the admin? Maybe that's the form that's being talked about in `todo`?

![3c514ce4b4bf3eb88c1e193655cf7b08.png](/assets/images/thm/thmchallenge/3.png)

Let's test this by sending an XSS payload

sent `<script>alert(1)</script>` in the content field

![3c514ce4b4bf3eb88c1e193655cf7b08.png](/assets/images/thm/thmchallenge/4.png)

Interesting, we can review the report? Let's see if our XSS fired!

![3c514ce4b4bf3eb88c1e193655cf7b08.png](/assets/images/thm/thmchallenge/5.png)

So XXS is in play. If the admin is checking, maybe we can steal the cookies?

I'm going to use `hookbin` and this payload:

![3c514ce4b4bf3eb88c1e193655cf7b08.png](/assets/images/thm/thmchallenge/6.png)

Sending that as the content of our request, let's see if we get anything on our `hookbin`

![3c514ce4b4bf3eb88c1e193655cf7b08.png](/assets/images/thm/thmchallenge/7.png)

Is that the cookie we want? Let's see what happens if we use that one instead of the one we have

![3c514ce4b4bf3eb88c1e193655cf7b08.png](/assets/images/thm/thmchallenge/8.png)

Now we can capture the flag :)

