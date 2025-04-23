---
title: SMTP (Simple Mail Transfer Protocol)
published: 2025-04-23
description: "SMTP"
image: "../../../assets/images/footprinting/footprinting.jpg"
tags: ["footprinting"]
category: Footprinting
draft: false
---
# SMTP (Simple Mail Transfer Protocol)

## 📧 Overview

- SMTP is a protocol used for sending emails over IP networks.
- It works in both:
    - Client ↔ Mail Server (email client sending to a server).
    - Server ↔ Server (mail transfer between SMTP servers).

## 🔌 Ports and Encryption

- Default Port: 25 (plain text).
- Secure Ports:
    - 587: Authenticated users with STARTTLS (upgrades to encrypted).
    - 465: SMTP over SSL/TLS.
- SMTP by default is unencrypted, transmitting data in plain text.
- STARTTLS is used to secure communication after connection starts.

## ✅ Authentication & Security

- Uses SMTP-Auth via ESMTP for authenticated sending.
- Only authorized users can send emails, preventing spam and abuse.
- Encrypted connections protect authentication data (username/password).

## 📤 Email Transmission Flow

- Mail User Agent (MUA): User's email client.
- Mail Submission Agent (MSA): Checks validity (relay server).
- Mail Transfer Agent (MTA): Sends/receives email, checks for spam.
- Mail Delivery Agent (MDA): Delivers to recipient’s mailbox (IMAP/POP3).
- Flow:
MUA ➞ MSA ➞ MTA ➞ MDA ➞ Mailbox

## 🚫 Challenges & Limitations

- No reliable delivery confirmation:
- SMTP returns basic English error messages if undelivered.
- Unauthenticated sender:
    - Easy to spoof sender address.
    - Open relays can be abused to send mass spam (Open Relay Attack).

## 🛡️ Security Techniques

- SPF (Sender Policy Framework): Verifies sender IP.
- DKIM (DomainKeys Identified Mail): Ensures message integrity.
- ESMTP: Modern extension that enables:
- STARTTLS (encryption after EHLO).
- AUTH PLAIN (safe authentication).

### Default Configuration

```
cat /etc/postfix/main.cf | grep -v "#" | sed -r "/^\s*$/d"
```

### SMTP Commands

- AUTH PLAIN
- HELO <hostname>
- EHLO <hostname>
- MAIL FROM:<sender>
- RCPT TO:<recipient>
- DATA
- RSET
- VRFY <username>
- EXPN <username>
- NOOP
- QUIT

### Connect to SMTP Server via Telnet

```
telnet <IP> 25
```

### Send an Email via Telnet

```
EHLO inlanefreight.htb
MAIL FROM:<sender>
RCPT TO:<recipient>
DATA
<email headers and body>
.
QUIT
```

### Proxy Command

```
CONNECT <IP>:25 HTTP/1.0
```

### Open Relay Misconfiguration

```
mynetworks = 0.0.0.0/0
```