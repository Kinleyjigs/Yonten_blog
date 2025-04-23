---
title: IMAP vs POP3 (Email Protocols)
published: 2025-04-23
description: "IMAP vs POP3"
image: "../../../assets/images/footprinting/footprinting.jpg"
tags: ["footprinting"]
category: Footprinting
draft: false
---
# IMAP vs POP3 (Email Protocols)

### ✉️ What is IMAP?

- IMAP (Internet Message Access Protocol) lets you manage your emails online directly on the mail server.
- It syncs emails across multiple devices.
- You can organize emails into folders on the server.
- Emails stay on the server unless you delete them.
- Great for accessing the same mailbox from different devices.

### ⚙️ How IMAP Works

- Connects to the server using port 143 (or 993 for secure SSL/TLS).
- Uses text-based commands (e.g., LOGIN, LIST, FETCH, LOGOUT).
- After login, emails can be browsed, read, and managed live on the server.
- Can work in offline mode with local copies that sync when online again.

### 📮 What is POP3?

- POP3 (Post Office Protocol v3) downloads emails from the server to your device and deletes them from the server by default.
- Mainly used for offline access.
- No folder support or multi-device sync.

### 🔒 Security Notes

- **IMAP & POP3 are unencrypted by default** (transmit data in plain text).
- Use **SSL/TLS encryption** (ports 993 for IMAP, 995 for POP3) for security.
- Avoid misconfigurations like logging passwords or allowing anonymous login.

### 🛠️ Testing & Configuration (Dovecot Example)

- Install using:
    
    `sudo apt install dovecot-imapd dovecot-pop3d`
    
- Dovecot allows customization and experimenting with services like IMAP/POP3.

### 📡 Common IMAP Commands

| Command | Description |
| --- | --- |
| LOGIN | Authenticate user |
| LIST | Show all folders |
| SELECT INBOX | Open mailbox |
| FETCH <ID> | Get email content |
| LOGOUT | Close connection |

### 📡 Common POP3 Commands

| Command | Description |
| --- | --- |
| USER / PASS | Login |
| LIST | List all emails |
| RETR ID | Download email |
| DELE ID | Delete email |
| QUIT | Close session |

### 🔍 Scanning with Nmap

- To scan for IMAP/POP3 services:

```
sudo nmap -sV -p110,143,993,995 -sC <target-ip>
```

- You can see open ports, capabilities, and certificate info (if SSL is used).

### 🧪 Testing Login via cURL

```
curl -k 'imaps://<ip>' --user user:password
```

- Use `v` for detailed output including TLS info.

### ⚠️ Dangerous Configurations

| Setting | Risk |
| --- | --- |
| `auth_debug` | Logs sensitive info |
| `auth_verbose_passwords` | Passwords may be exposed in logs |
| `auth_anonymous_username` | May allow anonymous access |