---
title: Security in Active Directory
published: 2025-04-29
description: "Security in Active Directory"
image: "./Why/image.png"
tags: ["Learning"]
category: Active Directory
draft: false
---

# Security in Active Directory

## Why is Active Directory considered insecure by default?

- **AD is built for sharing and fast access**, which makes it lean more toward **Availability and Confidentiality**, but **less on Integrity**.
- A default AD setup doesn’t have many security protections enabled. So, if left unchanged, it becomes an **easy target for attackers**.
- Security is about balancing **Confidentiality**, **Integrity**, and **Availability** (called the **CIA Triad**). In AD, Availability often wins, which may create **loopholes**.

## CIA Triad – The Foundation of Security

![alt text](<Security in Active Directory/image.png>)

- **Confidentiality** – Keeping data private and safe from unauthorized access.
- **Integrity** – Making sure data is not changed by anyone unauthorized.
- **Availability** – Making sure systems and data are always accessible to the right people.

**Active Directory focuses more on Availability and Confidentiality**, but sometimes that makes it less secure by default. So we need to take extra steps to improve security.

## General Hardening Measures for AD Security

These are **basic things every organization should do** to protect Active Directory from attacks:

### 1. **Microsoft LAPS (Local Administrator Password Solution)**

- This tool **automatically changes the local admin passwords** on all computers every few hours or days.
- Prevents attackers from using the same admin password across multiple machines.
- Even if one computer is hacked, others will still be safe.

### 2. **Audit Policy Settings (Logging & Monitoring)**

- You must **track and log all important events**, like:
    - New users or computers being added
    - Password changes
    - Unusual login activities
    - Use of hacking techniques like "password spraying" or "Kerberoasting"
- Helps detect and respond to attacks early.

### 3. **Group Policy Security Settings (GPOs)**

Group Policy lets you apply **security settings to many users and computers at once**.

Types of policies:

- **Account Policies**: Control passwords (length, complexity, lockout rules) and Kerberos ticket settings.
- **Local Policies**: Decide what users can do on their own computer (like install software, access USB).
- **Software Restriction Policies**: Stop users from running unsafe or unknown software.
- **AppLocker**: Block users from using dangerous tools like Command Prompt or PowerShell if they don’t need it.
- **Advanced Audit Policies**: Track activities like logging in, accessing files, or changing settings.

### 4. **Patch Management (WSUS / SCCM)**

- **Always keep Windows and AD systems updated**.
- Use tools like:
    - **WSUS** (free tool) to manage updates.
    - **SCCM** (paid tool with more features) for larger environments.
- Patching reduces the chance of attacks that exploit old vulnerabilities.

### 5. **Group Managed Service Accounts (gMSA)**

- Used for applications or services that need to log in automatically.
- These accounts:
    - **Have super long passwords (120 characters)**.
    - Are **automatically managed and rotated** by AD.
    - **No human needs to remember or know the password**.

### 6. **Security Groups**

- Instead of assigning permissions to users one by one, you put users in **security groups**.
- Examples: Admins, Backup Operators, Domain Users.
- Easier and safer to manage access to files, printers, folders, etc.

### 7. **Account Separation for Admins**

- Admins must use **two accounts**:
    - One for normal work (email, browsing)
    - One for admin tasks (AD, servers)
- If their daily account gets hacked, the attacker won’t automatically get access to admin powers.

### 8. **Password Policies & 2FA**

- Use **long passphrases or random passwords** (12+ characters).
- **Don’t use simple passwords** like "Welcome1" or "Password123".
- Use tools to **block common or weak passwords** (like months, seasons, company name).
- Always enable **2FA (Two-Factor Authentication)** – especially for remote access.

### 9. **Limit Use of Domain Admin Accounts**

- These accounts are extremely powerful.
- Only use them to:
    - Log into Domain Controllers
    - Do necessary admin tasks
- **Never use them to log into regular computers** – if those get hacked, the admin password could be stolen.

### 10. **Clean Up Old or Unused Accounts**

- Regularly check and **delete or disable accounts** that are:
    - Not used anymore
    - Belong to ex-employees
    - Have weak passwords
- Old forgotten accounts are **easy targets for attackers**.

### 11. **Audit Access Rights**

- Periodically check:
    - Who has access to what
    - Who is in the admin groups
    - If too many users have special privileges
- Keep it to the **minimum needed** for each person to do their job.

### 12. **Use Restricted Groups**

- Control group memberships using policies.
- For example:
    - Only allow Domain Admins and one local admin in every machine’s administrator group.
- Prevents unauthorized users from becoming admins.

### 13. **Limit Server Roles**

- Don't install multiple server roles (e.g., web server + domain controller) on the same system.
- Keep servers separate:
    - Web server = 1 machine
    - Database = another
    - Domain Controller = another
- This limits the damage if one server gets hacked.

### 14. **Restrict Local Admin & RDP Access**

- Carefully control:
    - Who can be a **local admin** on each computer.
    - Who can use **Remote Desktop (RDP)** to access computers.
- Don’t give Domain Users admin rights by default.
- Fewer people with access = fewer risks.