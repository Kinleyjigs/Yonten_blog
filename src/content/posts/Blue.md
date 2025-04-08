---
title: Blue
published: 2025-04-08
description: "How to use this blog template."
image: "../../assets/images/footprinting/footprinting.jpg"
tags: ["window machine"]
category: CTF Hack The Box
draft: false
---

# Blue

***window- easy machine*** 

# Enumeration

## Nmap

![alt text](<../../assets/images/CTF/Blue/image 1.png>)

the nmap scan shows up couple number of ports.

let’s try to see the vulnerabilities in port 445 as it is open for a Windows 7 version.

```notion
nmap -p 445 10.10.10.40 --script=smb-vuln-ms17-010.nse
```

![alt text](<../../assets/images/CTF/Blue/image 2.png>)

There is a code execution vulnerability in here and also provided a CVE for this version 

let’s try to find that one CVE using metasploit 

I search for the CVE and the target that is window7

![alt text](<../../assets/images/CTF/Blue/image 3.png>)

searched for the eternalblue 

![alt text](<../../assets/images/CTF/Blue/image 4.png>)

Then i found this [sl.no](http://sl.no) 24 that is a smb vulnerability.

Use that no.24 

![alt text](<../../assets/images/CTF/Blue/image 5.png>)

Then set the rhosts target machine ip 10.10.10.40.

Then hit exploit 

![alt text](<../../assets/images/CTF/Blue/image 6.png>)

Here i found that Host is likely VULNERABLE to MS17-010! - Windows 7 Professional 7601 Service Pack 1 x64 (64-bit)

Then i search for that exploit.

![alt text](<../../assets/images/CTF/Blue/image 7.png>)

Then hit use 0

again set the rhosts and lhost which is my localhosts ip.

![alt text](<../../assets/images/CTF/Blue/image 8.png>)

Then hits exploit again 

![alt text](<../../assets/images/CTF/Blue/image 9.png>)

Now i was able to enter inside the target machine’s  computer

![alt text](<../../assets/images/CTF/Blue/image 10.png>)

### User Flag

![alt text](<../../assets/images/CTF/Blue/image 11.png>)

### Root Flag

![alt text](<../../assets/images/CTF/Blue/image 12.png>)

### Machine completed

![alt text](<../../assets/images/CTF/Blue/image.png>)

## Learning
- improved on using metasploit
- exploit outdated versions.

## Reference

[https://www.youtube.com/watch?v=50ecL80v2LY](https://www.youtube.com/watch?v=50ecL80v2LY)