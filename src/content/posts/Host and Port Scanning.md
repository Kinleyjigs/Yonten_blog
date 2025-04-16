---
title: Host and Port Scanning
published: 2025-04-16
description: "Nmap port scans"
image: "../../assets/images/nmap/nmap.png"
tags: ["Scan", "Learning"]
category: Nmap
draft: false
---
# Host and Port Scanning

During the nmap scan we should look information like:

- Open ports and its services
- Service versions
- Information that the services provided
- Operating system

There are a total of 6 different states for a scanned port we can obtain:

![alt text](<../../assets/images/nmap/Host and Port Scanning/image.png>)

## Discovering Open TCP Ports

```markdown
sudo nmap 10.10.10.63 --top-ports=10
```

![alt text](<../../assets/images/nmap/Host and Port Scanning/image 1.png>)

![alt text](<../../assets/images/nmap/Host and Port Scanning/image 2.png>)

## Nmap - Trace the Packets

```markdown
sudo nmap 10.129.2.28 -p 21 --packet-trace -Pn -n --disable-arp-ping
```

![alt text](<../../assets/images/nmap/Host and Port Scanning/image 3.png>)

![alt text](<../../assets/images/nmap/Host and Port Scanning/image 4.png>)

## Request

![alt text](<../../assets/images/nmap/Host and Port Scanning/image 5.png>)

## Response

![alt text](<../../assets/images/nmap/Host and Port Scanning/image 6.png>)