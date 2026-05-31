---
title: DNS (Domain Name System)
published: 2025-04-23
description: "What is DNS?"
image: "../../../../assets/images/footprinting/footprinting.jpg"
tags: ["Learning"]
category: Footprinting
draft: false
---

# DNS (Domain Name System)

## 📍 What is DNS?

- DNS translates **domain names** (e.g., `www.hackthebox.com`) into **IP addresses**.
- It’s like the Internet’s **phonebook**, helping browsers find websites.
- DNS is **distributed** — no central database.
- Thousands of DNS servers globally share this data.

## 🌐 Types of DNS Servers

| **Type** | **Role** |
| --- | --- |
| **DNS Root Server** | Top-level; connects TLDs (e.g., `.com`, `.org`) with authoritative servers. 13 exist globally, managed by ICANN. |
| **Authoritative Nameserver** | Final authority for a DNS zone (e.g., `domain.com`). Responds with official DNS data. |
| **Non-authoritative Nameserver** | Not the main source. Gets info from others via recursive/iterative querying. |
| **Caching Server** | Temporarily stores DNS responses to reduce load and speed up queries. |
| **Forwarding Server** | Forwards queries to another DNS server. |
| **Resolver** | Often on your PC/router; starts the resolution process. Not authoritative. |

### 🔐 DNS Security

- DNS is **not encrypted** by default.
- Vulnerable to **spying, spoofing, MITM attacks**.
- Secure alternatives:
    - **DoT** (DNS over TLS)
    - **DoH** (DNS over HTTPS)
    - **DNSCrypt** (Encrypts DNS traffic)

### 🗂️ DNS Records

| **Record** | **Function** |
| --- | --- |
| `A` | IPv4 address |
| `AAAA` | IPv6 address |
| `MX` | Mail servers |
| `NS` | Name servers |
| `TXT` | Misc info (SPF, DMARC, Google verification) |
| `CNAME` | Alias for another domain |
| `PTR` | Reverse DNS — IP to domain |
| `SOA` | Zone info + admin email (`hostmaster@domain.com`) |

🧪 **Example**:

```
dig soa www.inlanefreight.com
```

### ⚙️ DNS Configuration (Bind9 Example)

### 1. Local Config Files (Main Control)

- `/etc/bind/named.conf.local`
- `/etc/bind/named.conf.options`
- `/etc/bind/named.conf.log`

📌 **Example**:

```
zone "domain.com" {
  type master;
  file "/etc/bind/db.domain.com";
  allow-update { key rndc-key; };
};
```

### 2. Zone Files (Forward Lookup)

📌 **Example**: `/etc/bind/db.domain.com`

```
$ORIGIN domain.com
@ IN SOA dns1.domain.com. hostmaster.domain.com. (
  2001062501 ; serial
  21600 ; refresh
  3600 ; retry
  604800 ; expire
  86400 ) ; minimum TTL
IN NS ns1.domain.com.
IN MX 10 mx.domain.com.
server1 IN A 10.129.14.5
www IN CNAME server2
```

### 3. Reverse Zone Files

📌 **Example**: `/etc/bind/db.10.129.14`

```
$ORIGIN 14.129.10.in-addr.arpa
@ IN SOA dns1.domain.com. hostmaster.domain.com. (
  2001062501 ; serial
  ...
)
5 IN PTR server1.domain.com.
```

### ⚠️ Dangerous Configurations (Security Risks)

| **Option** | **Description** |
| --- | --- |
| `allow-query` | Controls who can query the DNS server |
| `allow-recursion` | Controls who can use recursive lookups |

Misconfigurations (especially with `Bind9`) can:

- Leak data
- Allow DNS amplification attacks
- Create backdoors for attackers