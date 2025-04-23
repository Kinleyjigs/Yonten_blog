---
title: UTILIZING WHOIS
published: 2025-04-23
description: "Discovering Hidden Information"
image: "../../../assets/images/webinformation/webinfo.jpg"
tags: ["Web information"]
category: Web Information Gathering
draft: false
---
# WHOIS

it is used widely used to query databases that store information about registered internet resources

it can also provide info about IP address blocks and autonomous system. 

```python
[!bash!]$ whois inlanefreight.com

[...]
Domain Name: inlanefreight.com
Registry Domain ID: 2420436757_DOMAIN_COM-VRSN
Registrar WHOIS Server: whois.registrar.amazon
Registrar URL: https://registrar.amazon.com
Updated Date: 2023-07-03T01:11:15Z
Creation Date: 2019-08-05T22:43:09Z
[...]
```

each WHOIS record contain following info:

| **Field** | **Description** |
| --- | --- |
| **Domain Name** | The actual domain name (e.g., `example.com`). |
| **Registrar** | The company through which the domain was registered (e.g., GoDaddy, Namecheap). |
| **Registrant Contact** | The person or organization who owns or registered the domain. |
| **Administrative Contact** | The individual responsible for managing the domain. |
| **Technical Contact** | The person handling technical issues related to the domain. |
| **Creation & Expiration Dates** | The dates when the domain was registered and when it will expire. |
| **Name Servers** | Servers that resolve the domain name to its corresponding IP address. |

# **History of WHOIS**

The history of WHOIS is intrinsically linked to the vision and dedication of [Elizabeth Feinler](https://en.wikipedia.org/wiki/Elizabeth_J._Feinler), a computer scientist who played a pivotal role in shaping the early internet.

![image.png](WHOIS%2013cab0f53d1d80d09ef4cefadcd4b2c8/image.png)

# **Why WHOIS Matters for Web Recon**

During the reconnaissance phase of a penetration test, WHOIS records can offer valuable insights without directly interacting with the target. Here's how they help:

- **Identifying Key Personnel:** WHOIS records often list the names, email addresses, and phone numbers of individuals responsible for managing the domain. This information can be used to identify potential targets for social engineering attacks.
- **Uncovering Network Infrastructure:** Details such as IP addresses and name servers found in WHOIS data can reveal aspects of the target’s network setup. This helps penetration testers spot possible entry points or misconfigurations.
- **Analyzing Historical Records:** Services like WhoisFreaks provide access to historical WHOIS data, showing changes in ownership, contact info, or technical setup over time. This can help track how the target's digital footprint has evolved and uncover older, potentially weaker configurations.