---
title: FFuF Cheatsheet  
date: 2021-06-6
excerpt: "This is a Cheatsheet I created for reference when using FFuF"
classes: wide  
categories: cheatsheets  
tags:

- cheatsheets
- ffuf
---

# Switches

## Matching

- **-mc** - Match response codes
- **-ml** - match amount of lines in response
- **-mr** - Match regex pattern
- **-mw** - Match amount of words in response
- **-ms** - Match reponse size

## Filtering

- **-fc** - Filter response codes
- **-fl** - Filter by amount of lines in response
- **-fr** - Filter regex pattern
- **-fw** - Filter amount of words in response
- **-fs** - Filter response size

## Input

- **-mode** - Multi-wordlist operation mode. modes: **clusterbomb**, **pitchfork**
- **-request** - File containing the raw http request
- **-request-proto** - Protocol to use along with raw request
- **-w** - Wordlist

## Output

- **-o** - Output file
- **-of** - Output file format. (json, html, md, csv, all)

# Directory Busting

Generic

```
ffuf -w wordlist.txt -u http://site.com/FUZZ
```

File discovery using extensions

```
ffuf -w wordlist.txt -u http://site.com/FUZZ -e .php,.html
```

# VHOST

```
ffuf -w subdomains.txt -u http://site.com/ -H "Host: FUZZ.site.com"
```

# Login Forms

Generic

```
ffuf -w /wordlist -d "username=admin&password=FUZZ" -H "Content-Type: application/x-www-form-urlencoded" -u http://site.com/login
```

Clusterbomb and Pitchfork attacks

```
ffuf -u http://site.com/login -d "username=HFUZZ&password=WFUZZ" -H "Content-type: application/x-www-form-urlencoded" -mode clusterbomb -w usernames.txt:HFUZZ -w passwords.txt:WFUZZ
```

Clusterbomb and Pitchfork attacks with HTTP Request

request.txt:
```
POST /login HTTP/1.1
.
.
username=HFUZZ&password=WFUZZ
```

```
ffuf -request request.txt -request-proto http -mode clusterbomb -w usernames.txt:HFUZZ -w passwords.txt:WFUZZ
```

Clusterbomb is when every word in the username list will be used with every word in the password list

Pitchform is when the first line in the username list is used with the first line in the password list, 2:2, 3:3 etc
