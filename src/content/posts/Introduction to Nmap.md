---
title: Introduction to Nmap
published: 2025-04-16
description: "What is Nmap?"
image: "../../assets/images/nmap/nmap.png"
tags: ["Scan", "Learning"]
category: Nmap
draft: false
---

# Introduction to Nmap

### **What is Nmap?**

- **Open-source** network scanning and security auditing tool.
- Written in **C, C++, Python, and Lua**.
- Scans networks using **raw packets**.
- Detects:
    - Live hosts on the network
    - Running services and their versions
    - Operating systems and their versions
    - Firewall, IDS, and packet filter configurations
    

### **Key Use Cases**

Nmap is widely used by **network admins** and **security experts** for:

- 🔐 **Security auditing** of networks
- 🎯 **Simulated penetration testing**
- 🧱 **Firewall/IDS settings check**
- 🗺️ **Network mapping**
- 🔍 **Response and behavior analysis**
- 🛑 **Open port identification**
- ⚠️ **Vulnerability assessment**

### **Nmap Architecture**

1. **Host Discovery**
- Finds which devices are active on a network.

1. **Port Scanning**
- Identifies **open, closed, or filtered** ports on a target.

1. **Service Enumeration & Detection**
- Detects the services running on open ports.
- Also finds the **name and version** of the application.

1. **OS Detection**
- Identifies the **operating system and version** of the host.

1. **Nmap Scripting Engine (NSE)**
- Allows **custom scripts** for advanced scanning and exploitation.
- Useful for:
    - Vulnerability detection
    - Backdoor detection
    - Brute-forcing, etc.

### Scan Techniques

performing nmap —help gives us a 

```markdown
nmap --help
```

![alt text](<../../assets/images/nmap/Introduction to Nmap/image.png>)

### Nmap TCP-SYN Scan (-sS) – Simple Note.

![alt text](<../../assets/images/nmap/Introduction to Nmap/image 1.png>)

- Also called half-open scan.
- Default scan type in Nmap.
- Very fast and stealthy.
- Does not complete the full 3-way TCP handshake.