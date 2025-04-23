---
title: DIGGING DNS
published: 2025-04-23
description: "DNS"
image: "../../../assets/images/webinformation/webinfo.jpg"
tags: ["Web information"]
category: Web Information Gathering
draft: false
---

# DIGGING DNS

# **DNS Tools**

DNS reconnaissance involve utilizing specialized tools designed to query DNS server and extract valuable information. 

| Tool | What It Does | When to Use |
| --- | --- | --- |
| `dig` | Versatile DNS query tool with detailed output | Manual lookups, record analysis, troubleshooting |
| `nslookup` | Simple DNS lookup tool | Quick checks for A, AAAA, MX records |
| `host` | Streamlined DNS queries | Fast A, AAAA, MX lookups |
| `dnsenum` | Automated subdomain and DNS enumeration with dictionary & brute force | Discovering subdomains, zone transfers (if allowed) |
| `fierce` | DNS recon with wildcard detection and recursive search | Mapping subdomains, scanning DNS infrastructure |
| `dnsrecon` | Combines multiple recon techniques, supports output formats | In-depth DNS recon, exportable results |
| `theHarvester` | Gathers DNS, emails, and more from public sources | OSINT, finding emails/domains related to a company |
| **Online Tools** | Web-based interfaces for DNS queries | Quick checks when terminal access isn’t available |

# **The Domain Information Groper**

dig command (Domain Information Groper) a versatile tool used to query DNS server and retrieving various type of record 

### **Common dig Commands**

| Command | What It Does | When to Use |
| --- | --- | --- |
| `dig domain.com` | Basic DNS lookup (A record) | To get IPv4 address of a domain |
| `dig domain.com A` | Queries only A (IPv4) record | When specifically checking IPv4 address |
| `dig domain.com AAAA` | Queries AAAA (IPv6) record | When checking IPv6 support |
| `dig domain.com MX` | Queries mail exchange records | To find mail servers |
| `dig domain.com NS` | Queries authoritative name servers | To see which DNS servers manage the domain |
| `dig domain.com TXT` | Gets text records | Useful for SPF, DKIM, and verification strings |
| `dig domain.com CNAME` | Finds canonical name alias records | To check if a domain is an alias |
| `dig domain.com SOA` | Gets Start of Authority record | To see domain's primary DNS and serial info |
| `dig @1.1.1.1 domain.com` | Uses a specific DNS server (1.1.1.1 in this case) | When testing DNS resolution from different NS |
| `dig +trace domain.com` | Traces DNS path from root to domain | For understanding full DNS resolution path |
| `dig -x <IP>` | Reverse DNS lookup (IP → Domain) | To find domain name from an IP address |
| `dig +short domain.com` | Returns just the IP(s) or value(s) of the record | Clean, script-friendly output |
| `dig +noall +answer domain.com` | Shows only the answer section | To reduce noise and focus on results |
| `dig domain.com ANY` | Requests all available records | Use with caution – may be blocked by servers |

Caution: Some servers can detect and block excessive DNS queries. Use caution
and respect rate limits. Always obtain permission before performing extensive
DNS reconnaissance on a target.