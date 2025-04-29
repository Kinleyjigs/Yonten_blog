---
title: User and Machine Accounts
published: 2025-04-29
description: "User and Machine Accounts"
image: "./Why/image.png"
tags: ["Learning"]
category: Active Directory
draft: false
---

# User and Machine Accounts

## **Purpose of User Accounts**

User accounts (local or domain) allow individuals or programs to:

- Log on to systems
- Access system resources
- Execute tasks under specific security contexts

Upon login:

- The system verifies the password
- Generates an **access token** containing:
    - Security identifier (SID)
    - Group membership
    - Rights and privileges

These tokens govern access to system resources throughout a session.

## **Why User Accounts Matter**

- Users can be assigned to **groups** to manage access more efficiently.
- Administrators can assign privileges at the **group level** instead of individually.
- Helps with:
    - Simplified access control
    - Easier privilege revocation
    - Reduced risk of misconfigurations

## **User Account Types**

### a. **Standard User Accounts**

- Used by employees or contractors
- Typically part of `Domain Users` group
- Can be:
    - Local accounts (for non-domain systems)
    - Domain accounts (for enterprise environments)

### b. **Admin Accounts**

- Elevated privileges for system administration
- E.g., IT support, system admins, help desk technicians

### c. **Service Accounts**

- Used to run background services or applications
- Often highly privileged
- Must be carefully managed to prevent misuse

### d. **Disabled Accounts**

- Belong to former employees or temporary staff
- Often retained for **audit purposes**
- Typically moved to special OUs like `Former Employees`
- Should be deactivated and stripped of privileges

## **Active Directory (AD) User Accounts**

- Every user in an organization typically has at least one AD account.
- Large organizations may have more accounts than actual users.
- AD helps centralize:
    - User provisioning
    - Access control
    - Group policy management

## **Security Risks of User Accounts**

- **Misconfigurations** can grant unintended privileges
- Often the **primary attack vector** in penetration testing
- Common issues:
    - Weak passwords
    - Password reuse
    - Poor privilege management
    - Lack of account auditing

Organizations should adopt:

- Security policies
- User behavior monitoring
- Defense-in-depth strategies

## **Local Accounts**

Stored **locally** on a device (not domain-joined):

- Only valid for that machine
- Can manage resources on that host

- Examples of default local accounts:

| Account | Description |
| --- | --- |
| **Administrator** | Full control over the host. Cannot be deleted/locked. Usually disabled by default on new Windows systems. |
| **Guest** | Temporary, limited access. Disabled by default. Security risk if enabled. |
| **SYSTEM (NT AUTHORITY\SYSTEM)** | OS-level account with the highest privileges. Cannot be deleted, does not appear in User Manager. Used internally by Windows. |
| **Network Service** | Used to run services with limited privileges. Presents computer credentials to network. |
| **Local Service** | Runs services with minimal privileges. Presents anonymous credentials to network. |

## **Domain Users**

- Centralized in Active Directory
- Can access shared resources across the domain:
    - File servers
    - Intranet
    - Printers
- Managed via **Group Policy**

## Key AD User Naming Attributes

| Attribute | Description |
| --- | --- |
| **UserPrincipalName (UPN)** | Typically the user's email address, used for login |
| **ObjectGUID** | Globally unique identifier for the user object |
| **SAMAccountName** | Legacy logon name, used by older systems |
| **objectSID** | Unique Security Identifier assigned to the user |
| **sIDHistory** | Stores previous SIDs, helpful in domain migrations |

### **Example: AD User Attributes**

Command: `Get-ADUser -Identity htb-student`

| Attribute | Value |
| --- | --- |
| DistinguishedName | CN=htb student,CN=Users,DC=INLANEFREIGHT,DC=LOCAL |
| Enabled | True |
| GivenName | htb |
| Name | htb student |
| ObjectGUID | `aa799587-c641-4c23-a2f7-75850b4dd7e3` |
| SamAccountName | `htb-student` |
| SID | `S-1-5-21-3842939050-3880317879-2865463114-1111` |
| Surname | student |
| UserPrincipalName | `htb-student@INLANEFREIGHT.LOCAL` |

### **KRBTGT Account (Special Case)**

- A service account for the **Kerberos Key Distribution Center (KDC)**
- Vital for domain authentication
- **Highly targeted** in attacks (e.g., Golden Ticket)
- Compromise of this account grants **unrestricted domain access**

## Domain-Joined vs Non-Domain-Joined Machines

| Category | Domain-Joined | Non-Domain-Joined (Workgroup) |
| --- | --- | --- |
| **Management** | Centralized via AD and Group Policy | Managed locally per machine |
| **Resource Access** | Users can log in from any domain host | Access limited to local host |
| **Typical Use** | Enterprise environments | Home, small offices |
| **Configuration** | Policy-based and unified | Manual configuration required |
| **Profiles** | Roaming or portable | Tied to local machine |

## **Machine Accounts in AD**

- Machine accounts are created in AD when a system joins the domain
- SYSTEM-level access on domain-joined hosts can be leveraged to:
    - Enumerate domain data
    - Launch AD-related attacks
- SYSTEM access is a **powerful foothold**, not just for local exploitation