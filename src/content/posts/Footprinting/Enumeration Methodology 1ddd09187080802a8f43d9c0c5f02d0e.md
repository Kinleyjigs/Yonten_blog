---
title: Enumeration Methodology
published: 2025-04-23
description: "Enumeration Model"
image: "../../../assets/images/footprinting/footprinting.jpg"
tags: ["Learning"]
category: Footprinting
draft: false
---
# Enumeration Methodology

## 🧭 Purpose of the Methodology

- Enumeration is a **critical phase** in penetration testing.
- Due to the **complex and dynamic nature** of systems, a **structured approach** prevents missing vital components.
- Penetration testers often use **experience-based workflows**, but this can lead to inconsistency.
- Hence, a **static yet adaptable methodology** is needed for both **external and internal penetration tests**.

## 🧱 The 6-Layer Enumeration Model

Think of each layer like a **wall or barrier** we need to pass to move deeper into the system, each with potential “gaps” (vulnerabilities).

**Level 1**: Infrastructure-Based Enumeration

**Level 2**: Host-Based Enumeration

**Level 3**: OS-Based Enumeration

## 🔐 Layer Descriptions & Key Focus Areas

| Layer | Description | Focus Information |
| --- | --- | --- |
| **1. Internet Presence** | Find the company’s presence on the internet. | Domains, Subdomains, vHosts, ASN, Netblocks, IPs, Cloud Instances, Security Measures |
| **2. Gateway** | Understand the protective mechanisms in place. | Firewalls, DMZ, IDS/IPS, EDR, Proxies, NAC, VPN, Cloudflare |
| **3. Accessible Services** | Identify available services and their functions. | Service Type, Port, Version, Interface, Configuration |
| **4. Processes** | Understand internal service-related processes. | PID, Tasks, Data Sources, Data Destinations |
| **5. Privileges** | Find out user roles and permission levels. | Users, Groups, Permissions, Restrictions, Environments |
| **6. OS Setup** | Investigate the OS configuration and setup. | OS Type, Patch Level, Network Config, Sensitive Files |

## 🧩 Real-Life Analogy: The Labyrinth

- Think of a **penetration test as a maze** with many possible entry points.
- Not every discovered gap leads to deeper access.
- Time is limited — **choosing the right path is critical**.
- Even after weeks of testing, **undiscovered vulnerabilities may remain**.
- Example: The **SolarWinds attack** proved deep, long-term access is sometimes needed to uncover weaknesses.

### 🛠️ Methodology vs. Tools

- **Methodology** = **Systematic approach** to explore the target.
- **Tools** = Practical aids or cheat sheets to execute parts of the methodology.
    - Tools change over time, but the **goal remains the same**: effective information gathering.

### 🧠 Final Thoughts

- The methodology is **not a step-by-step guide**, but a **flexible framework**.
- Always adapt based on the **scope, target, and available time**.
- Remember: **There's (almost) always a way in.** 🕵️‍♂️