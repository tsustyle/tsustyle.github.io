---
title: Granny & Grandpa
date: 2021-01-27
excerpt: "Granny & Grandpa are a pair of identical easy rated boxes on Hack the Box. We'll use metasploit to exploit a buffer overflow in IIS 6.0/WebDav for access and a kernel exploit for privesc"
classes: wide
categories: HackTheBox 
tags:
  - htb
  - windows
  - IIS
  - WebDav
  - metasploit
---

![img](/assets/images/htb/grannygrandpa/header.png)

### Port Scanning and General Enumeration (Nmap, Nikto)
* Reading/Resources
  * [Nmap manual](https://nmap.org/book/man.html)

Initial scan showed just 80 (HTTP) open


![img](/assets/images/htb/grannygrandpa/0.png)


![img](/assets/images/htb/grannygrandpa/1.png)

Gobuster returned nothing. Nikto had a bunch to say, but I'm starting to see a trend. `WebDav` in the nmap scan, `WebDav` in the nikto scan


![img](/assets/images/htb/grannygrandpa/2.png)

### Things we know
- IIS 6.0
- WebDav is enabled


---

### Access (searchsploit, metasploit)
* Reading/Resources
  * [searchsploit](https://www.exploit-db.com/searchsploit)
  * [metasploit](https://www.metasploit.com/)

Searchsploit:


![img](/assets/images/htb/grannygrandpa/3.png)

WebDav remote buffer overflow? There's a python script, but I couldn't get it to work. Let's check out `metasploit`


![img](/assets/images/htb/grannygrandpa/4.png)

That's what we're looking for!


![img](/assets/images/htb/grannygrandpa/5.png)


![img](/assets/images/htb/grannygrandpa/6.png)

And we're in!

---

### Privesc (metasploit, kitrap0d)
* Reading/Resources
  * [metasploit](https://www.metasploit.com/)
  * [kitrap0d](https://www.exploit-db.com/exploits/11199)
  
Running into issues with my shell and running post exploits. Something about insufficient privileges so I tried migrating to a different process


![img](/assets/images/htb/grannygrandpa/7.png)


![img](/assets/images/htb/grannygrandpa/8.png)

new process seems to work

`use post/multi/recon/local_exploit_suggester`


![img](/assets/images/htb/grannygrandpa/9.png)

Let's try `kitrap0d`


![img](/assets/images/htb/grannygrandpa/10.png)

That got us there


![img](/assets/images/htb/grannygrandpa/11.png)


![img](/assets/images/htb/grannygrandpa/12.png)
