---
title: Why
published: 2025-04-29
description: "Active Directory"
image: "./Why/image.png"
tags: ["Learning"]
category: Active Directory
draft: false
---

# Why

## What is Active Directory (AD)?

- AD is a system made by Microsoft to **manage everything** (users, computers, groups, files, etc.) inside a **Windows network**.
- It’s **organized like a tree** (hierarchical) and **spread across different servers** (distributed).
- AD makes it easier for administrators to control who can access what.

## **What Does AD Do?**

- **Authentication**: Checks if you are who you say you are.
- **Authorization**: Decides what you are allowed to do after logging in.

## **Why is AD Important and Also Risky?**

- **Very common target** for hackers because:
    - It was made to support old systems (**backward-compatible**), so some features are **not secure by default**.
    - It's **easy to misconfigure** (set up wrongly) and leave holes for attackers.
- If AD is not protected well, hackers can **move around** inside the network (lateral movement) or **gain higher-level access** (vertical movement).

## **Who Can Access AD?**

- **Every user** (even normal, low-level users) can **see a lot of information** inside AD.
- A basic user can:
    - List (enumerate) almost all objects in AD.
    - Find weak spots to attack.
- **This is dangerous** because even one small account can cause big problems if AD is not secured properly.

## 🔒**How to Protect AD**

- **Defense-in-Depth**: Use many layers of security, not just one.
- **Plan Carefully**: Think ahead about security when setting up AD.
- **Network Segmentation**: Break the network into parts so attackers can't easily move everywhere.
- **Least Privilege**: Give users only the access they *really* need — no more.

## **Example of an Attack**

![alt text](<Why/image 1.png>)

- **noPac Attack** (December 2021):
    - A big security flaw where attackers could gain control of the domain using just a normal user account.
    - Showed how dangerous misconfigurations in AD can be.

## **Importance of Active Directory**

- Around **95% of Fortune 500 companies** use Active Directory.
- AD is a **key target** for attackers.
- A **phishing attack** that gives an attacker access as a **standard domain user** is enough to:
    - Start **mapping the domain**.
    - **Find attack paths**.

## **AD and Ransomware Attacks**

- **Ransomware operators** increasingly target Active Directory.
- Example: **Conti Ransomware** (involved in 400+ attacks globally):
    - Exploited **PrintNightmare** (CVE-2021-34527) and **Zerologon** (CVE-2020-1472).
    - Used these to:
        - **Escalate privileges**.
        - **Move laterally** across networks.
- Understanding AD structure is **critical** to find and fix flaws **before attackers do**.

## **Why Learning AD is Essential**

- **New critical attacks** are discovered frequently.
- Sometimes **only standard user access** is enough for **full domain takeover**.
- Open-source tools exist for AD attacks, but:
    - Their effectiveness depends on **user knowledge of AD**.
- Deep understanding helps:
    - **Identify obvious and hidden flaws**.
    - **Perform better enumeration and attacks**.
    - **Defend and fix environments effectively**.

## **What This Module Covers**

- **Foundations for Active Directory enumeration and attacks**.
- Topics included:
    - **AD structure and function**.
    - **Different AD objects**.
    - **User rights and privileges**.
    - **Tools and processes** for managing AD.
    - **Hands-on setup** of a small Active Directory environment.

# **History of Active Directory**

## **Early Developments**

- **LDAP** (Lightweight Directory Access Protocol):
    - Introduced via RFCs around **1971**.
- **X.500 Organizational Unit Concept**:
    - Early version of directory systems.
    - Developed by **Novell and Lotus** (1993 → Novell Directory Services).

## **Microsoft's Journey**

- **Early attempts (1990)**:
    - **Windows NT 3.0** was a mix of:
        - **LAN Manager protocol**.
        - **OS/2 operating system** (jointly developed with IBM).
    - Led by **Ed Iacobucci** (also co-founder of **Citrix Systems**).
- **Evolution through the 1990s**:
    - Adopted protocols like **LDAP** and **Kerberos**.
    - Added Microsoft’s proprietary technologies.
- **First Beta of AD**: Released in **1997**.
- **Official Launch**:
    - AD became part of **Windows Server 2000**.

## **Major Releases and Features**

| Version | Features |
| --- | --- |
| **Windows Server 2003** | - Extended AD functionality. - Introduced **Forest feature**: Separate domains, users, computers under one container. |
| **Windows Server 2008** | - Introduced **Active Directory Federation Services (ADFS)**. - Enabled **Single Sign-On (SSO)** for systems and applications. - Used **claims-based access control authorization**. |
| **Windows Server 2016** | - Focused on **cloud migration**. - Introduced **Group Managed Service Accounts (gMSA)** for better security (e.g., against **Kerberoasting**). - Launched **Azure AD Connect** for Office 365 SSO. |

# **Challenges with Active Directory**

## **Misconfigurations and Vulnerabilities**

- AD has been vulnerable to **misconfigurations** and **new exploits** since 2000.
- Related technologies like **Microsoft Exchange** also impact AD security.

## **Responsibilities of Security Professionals**

- As **penetration testers** or **defenders**, must:
    - **Identify vulnerabilities** before real attackers do.
    - Understand:
        - **AD structure**.
        - **Protocols (LDAP, Kerberos, etc.)**.
        - **User rights management**.
        - **AD administration methods**.
        - **Common misconfigurations**.
- **Managing AD is complex**:
    - Fixing one issue can **create new problems elsewhere**.

# **Current and Future Importance**

## **On-Premises Active Directory**

- Despite **cloud migrations**, **on-premises AD** will continue to exist.
- **Network penetration tests** almost always encounter some form of AD.

## **Benefits of Deep AD Knowledge**

- Easier to **attack and defend** environments of all sizes.
- Increases **confidence** when facing:
    - **Small environments** (20 machines).
    - **Large environments** (10,000+ machines).
- Helps in giving **effective remediation advice** to clients.