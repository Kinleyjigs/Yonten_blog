---
title: SUBDOMAIN BRUTE-FORCING
published: 2025-04-23
description: "Discovering Hidden Information"
image: "../../../assets/images/webinformation/webinfo.jpg"
tags: ["Web information"]
category: Web Information Gathering
draft: false
---
# SUBDOMAIN BRUTE-FORCING

subdomain brute-forcing enumeration is powerful technique that use pre-defined wordlists to identify valid subdomain enhancing the effectiveness of discovery of subdomain

the process breaks down in four steps:

1. Wordlist Selection: it starts with selecting the right wordlist containing potential subdomain name
    - general-purpose: containing a board range of common subdomain name, when we don’t have any idea about the target
    - Targeted: relevant to target
    - Custom: we can create our own wordlist based on keywords, etc
2. Iteration and Querying: scripts that checks the wordlist for searching subdomain
3. DNS Lookup: A DNS checks if each potential subdomain resolves to an IP address, typically done by using the A or AAA
4. Filtering and Validation: successfully resolving subdomain are added to a list of valid one, and testing through browsing to ensure that it works

There are several tools available that excel at brute-force enumeration:

| **Tool** | **Description** | **When to Use** |
| --- | --- | --- |
| **dnsenum** | Comprehensive tool with dictionary and brute-force support for subdomain discovery. | When you need thorough subdomain discovery using wordlists. |
| **fierce** | User-friendly tool for recursive subdomain lookups with wildcard detection. | For mapping subdomains quickly with minimal setup. |
| **dnsrecon** | Combines multiple DNS recon techniques; supports various output formats. | When performing full-scale DNS recon and need exportable results. |
| **amass** | Actively maintained; integrates well with APIs and other tools, wide range of data sources. | For advanced subdomain enumeration at scale. |
| **assetfinder** | Lightweight and fast tool using passive sources for subdomain discovery. | For quick scans using passive OSINT data. |
| **puredns** | Fast, accurate brute-force tool for resolving domains and filtering wildcards. | When doing high-performance brute-forcing with clean results. |

### **DNSEnum**

- DNS Record Enumeration: dnsenum can retrieve various records, including A, AAA, NS, MX and TXT records, providing overview of DNS configuration.
- Zone Transfer Attempts: the tool tries to get zone transfer from found server, though most server block unauthorized transfer, a successful attempt can provide valuable information
- Subdomain Brute-Forcing: dnsenum supports brute-force enumeration of subdomains using wordlist.
- Google Scraping: the tool searches Google results to find extra subdomain that may not appear in DNS records
- Reverse Lookup: dnsenum can check which domains are linked to a specific IP address, uncovering other website on the same server.
- WHOIS Lookup: the tool can also performs WHOIS lookup to find who owns the domain and its registration info

subdomains-top1million-5000.txt ⇒ wordlist from Seclist 

demonstrating how dnsenum enumerate subdomain 

```python
dnsenum --enum inlanefreight.com -f /usr/share/seclists/Discovery/DNS/subdomains-top1million-110000.txt -r
```

- dnsenum --enum [inlanefreight.com](http://inlanefreight.com/): specify the target with shortcut options —enum
- -f /usr/share/seclists/Discovery/DNS/subdomains-top1million-5000.txt: specify the wordlist
- -r: this options is for recursive subdomain brute-forcing, if dnsenum  finds subdomain, it will try to enumerate subdomain to that subdomain