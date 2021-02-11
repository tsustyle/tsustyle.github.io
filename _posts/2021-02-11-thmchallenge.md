MyChallenge

![3c514ce4b4bf3eb88c1e193655cf7b08.png](../../_resources/fd816dc633e140848f39bde6f7126358.png)

`/robots.txt` has some Disallows

```
User-agent: *
Disallow: /admin
Disallow: /todo
```

Admin is a rabbithole. `todo` actually has some info.

![8b4f3725bc5fa025f7a70e7b8c46371b.png](../../_resources/0e329c25c0e64b6d9dfe0fa7b974e62f.png)

Looks like there's a new feature that hasn't been sufficiently tested for security holes.

Register an account to get a look at the member's area

![750035ed6f607645ac46fc89ea3fc434.png](../../_resources/dd8d5666c6744464be94ad772edae777.png)

So we can upload a resume or send a request to the admin? Maybe that's the form that's being talked about in `todo`?

![34f9b8c9d18baed3eb582f6d517162c7.png](../../_resources/c5fa9df1595843038118150109da7588.png)

Let's test this by sending an XSS payload

sent `<script>alert(1)</script>` in the content field

![b37b329efc0c738c942ef8d5afcacc4c.png](../../_resources/0db0ae54fbdb425fb45b477877cc02be.png)

Interesting, we can review the report? Let's see if our XSS fired!

![bc2625f333b31f96b963d9f83b458caf.png](../../_resources/bb8eaa1711a045da802a4e476b596079.png)

So XXS is in play. If the admin is checking, maybe we can steal the cookies?

I'm going to use `hookbin` and this payload:

![688f8f59a9db4775e070fa977e5c3997.png](../../_resources/ee05dbe1a2e84ab3aa896fd88ff6b708.png)

Sending that as the content of our request, let's see if we get anything on our `hookbin`

![3a18210014f9c299ff8bdeb95ced50ad.png](../../_resources/bd6d363e7b0b4f67bb823645d06db2c5.png)

Is that the cookie we want? Let's see what happens if we use that one instead of the one we have

![ab23366ede12e14b161be88b06d3c7c1.png](../../_resources/1848d2ad398d4869a5586a018e79cbd0.png)

Now we can capture the flag :)

