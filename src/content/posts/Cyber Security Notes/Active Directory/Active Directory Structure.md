---
title: Active Directory Structure
published: 2025-04-29
description: "Active Directory"
image: "./Why/image.png"
tags: ["Learning"]
category: Active Directory
draft: false
---

# Active Directory Structure

- Active Directory (AD) is a directory service for Windows networks that helps manage users, computers, groups, and resources.
- It provides authentication and authorization, storing information like usernames and passwords.
- AD allows both users and administrators to access network resources and was first introduced with Windows Server 2000. However, it can be difficult to manage securely, especially in large environments, and is often targeted by attackers.

### AD flaws and misconfigurations can allow:

- Internal access (foothold)
- Lateral and vertical movement in the network
- Unauthorized access to databases, file shares, source code, etc.

### AD is like a large, searchable database:

- Even basic users can enumerate important objects:
    - Domain Computers
    - Domain Users
    - Domain Groups
    - Organizational Units (OUs)
    - Group Policy Objects (GPOs)
    - Password Policies
    - Domain Trusts
    - Access Control Lists (ACLs)

### AD Structure:

- **Forest** → Top-level security boundary; contains domains.
- **Domains** → Hold users, computers, groups.
- **Subdomains** → Child domains under a domain.
- **Organizational Units (OUs)** → Organize objects and apply group policies.
    - OUs can have objects and nested sub-OUs.

### Example of a very (simplistic) high level, an AD structure:

```notion
INLANEFREIGHT.LOCAL/
├── ADMIN.INLANEFREIGHT.LOCAL
│ ├── GPOs
│ └── OU
│ └── EMPLOYEES
│ ├── COMPUTERS
│ │ └── FILE01
│ ├── GROUPS
│ │ └── HQ Staff
│ └── USERS
│ └── barbara.jones
├── CORP.INLANEFREIGHT.LOCAL
└── DEV.INLANEFREIGHT.LOCAL
```

### **Domains and Trusts in Active Directory:**

- **INLANEFREIGHT.LOCAL** is the **root domain**.
- Subdomains under it:
    - **ADMIN.INLANEFREIGHT.LOCAL**
    - **CORP.INLANEFREIGHT.LOCAL**
    - **DEV.INLANEFREIGHT.LOCAL**
- Domains include:
    - Users
    - Groups
    - Computers
    - Other directory objects
- **Trust Relationships:**
    - Common in organizations with acquisitions.
    - Easier to create trusts than to recreate users in a new domain.
    - Trusts allow users in one domain to access resources in another.
- **Security Note:**
    - Improperly managed trusts can introduce **security risks**.

![alt text](<Active Directory Structure/image.png>)

### INLANEFREIGHT.LOCAL and FREIGHTLOGISTICS.LOCAL

![alt text](<Active Directory Structure/image 1.png>)

- **Bidirectional Trust Between Forests**:
    - There is a bidirectional trust established between the root domains of `INLANEFREIGHT.LOCAL` and `FREIGHTLOGISTICS.LOCAL`. This means:
        - A user in the `INLANEFREIGHT.LOCAL` forest can access resources in `FREIGHTLOGISTICS.LOCAL`, and vice versa.
- **Child Domains and Trusts**:
    - Both `INLANEFREIGHT.LOCAL` and `FREIGHTLOGISTICS.LOCAL` have multiple child domains. However, the child domains within one forest (e.g., `admin.dev.freightlogistics.local` and `wh.corp.inlanefreight.local`) do not automatically have trusts with child domains in the other forest.
- **Authentication Issues Across Forests**:
    - In your example:
        - A user from `admin.dev.freightlogistics.local` cannot authenticate directly to machines in `wh.corp.inlanefreight.local` by default, even though the top-level root domains (`INLANEFREIGHT.LOCAL` and `FREIGHTLOGISTICS.LOCAL`) have a bidirectional trust.
        - This is because the trust does not extend to child domains unless specifically configured.
- **Solution (Creating Additional Trusts)**:
    - To enable users in `admin.dev.freightlogistics.local` to authenticate on `wh.corp.inlanefreight.local`, a **secondary trust** would need to be created between the specific child domains: `admin.dev.freightlogistics.local` and `wh.corp.inlanefreight.local`.
    - This means the trust configuration needs to account for not only the root domains but also any child domains that need cross-forest authentication or resource access.