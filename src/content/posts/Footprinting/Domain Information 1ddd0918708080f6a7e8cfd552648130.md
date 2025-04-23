---
title: Domain Information
published: 2025-04-23
description: "Domain Information & Passive Recon"
image: "../../../assets/images/footprinting/footprinting.jpg"
tags: ["Learning"]
category: Footprinting
draft: false
---
# Domain Information

### 🌐 Domain Information & Passive Recon

- Domain info is more than just subdomains — it’s about understanding the **company’s entire internet presence**.
- We gather this data **passively** (no direct contact), acting like regular users or customers.
- This involves:
    - Checking the **main website**
    - Noting **technologies used**
    - Understanding **services offered** (e.g., IoT, app dev, data science, etc.)
    

🧠 Tip: Services give clues about the company’s internal structure and tech setup.

- If we don’t know a service, we research it to learn its **technical requirements**.
- This helps us "see what’s not shown" — the **hidden functionality** behind services.

🔍 We combine both principles of enumeration:

1. **What we see** (public services)
2. **What we don’t see** (how those services function technically)

### 🔍 **Online Presence Enumeration**

### 🧩 **Initial Setup**

- Assume we're testing a company as a **black-box pentester**:
    
    We only have the **target domain** – no internal info.
    

### 🔐 **SSL Certificates (Certificate Transparency Logs)**

- SSL certs can reveal **multiple subdomains** used by a company.
- Use [crt.sh](https://crt.sh/) to search certificates for a domain.
    
    Example:
    
    ```markdown
    curl -s "https://crt.sh/?q=inlanefreight.com&output=json" | jq .
    ```
    

- Helps find subdomains like:
[matomo.inlanefreight.com](http://matomo.inlanefreight.com/), [smartfactory.inlanefreight.com](http://smartfactory.inlanefreight.com/), etc.

### 🌐 Subdomain Discovery

Use [crt.sh](http://crt.sh/) output or tools like amass, assetfinder, or subfinder.

Filter out unique subdomains:

```markdown
curl ... | jq . | grep name
```

### 🖥️ **Identify Company-Hosted Servers**

- Check which subdomains resolve to **internal IPs**:

```markdown
for i in $(cat subdomainlist); do host $i | grep "has address" | grep inlanefreight; done
```

### 🔎 **Use Shodan to Analyze IPs**

- Shodan reveals info like open ports, location, and services.

```markdown
for i in $(cat ip-addresses.txt); do shodan host $i; done
```

Example findings:

- IP: 10.129.27.33
- Ports: 22 (SSH), 80 (HTTP), 443 (HTTPS)
- Location: Berlin
- Org: InlaneFreight

**🧠 Remember Key Targets**
Keep note of interesting IPs like 10.129.127.22 for later testing.

### 📡 Check DNS Records

- Use dig to list records for the domain:

```markdown
dig any inlanefreight.com
```

Look for:

- A Records (IP addresses)
- MX Records (Mail servers)
- NS Records (Name servers)