---
title: Active Directory Functionality
published: 2025-04-29
description: "Active Directory"
image: "./Why/image.png"
tags: ["Learning"]
category: Active Directory
draft: false
---

# Active Directory Functionality

### five Flexible Single Master Operation (FSMO) roles.

| **Role** | **Description** |
| --- | --- |
| **Schema Master** | Manages the read/write copy of the Active Directory **schema**, which defines all object classes and attributes in AD. Only one schema master exists per forest. |
| **Domain Naming Master** | Ensures **unique domain names** across the forest and manages additions/removal of domains. Prevents creation of duplicate domain names. Only one per forest. |
| **Relative ID (RID) Master** | Assigns blocks of **RIDs** to DCs within a domain to ensure **unique SIDs** for each object. Prevents duplication of object SIDs. Only one RID Master per domain. |
| **PDC Emulator** | Acts as the **Primary Domain Controller**. Handles time synchronization, password changes, account lockouts, and Group Policy updates. Responds to legacy authentication requests. One per domain. |
| **Infrastructure Master** | Translates **GUIDs, SIDs, and DNs** between domains. Essential for proper display of cross-domain object names in multi-domain forests. Only one per domain (not needed if all DCs are GCs). |

### Domain and Forest Functional Levels

| **Domain Functional Level** | **Features Available** | **Supported Domain Controller Operating Systems** |
| --- | --- | --- |
| **Windows 2000 Native** | - Universal groups (distribution and security)
- Group nesting
- Group conversion
- SID history | Windows Server 2008 R2, 2008, 2003, 2000 |
| **Windows Server 2003** | - **netdom.exe** domain management
- **lastLogonTimestamp** attribute
- Well-known users and computers containers
- Constrained delegation
- Selective authentication | Windows Server 2012 R2, 2012, 2008 R2, 2008, 2003 |
| **Windows Server 2008** | - DFS replication for SYSVOL
- AES 128/256 support for Kerberos
- Fine-grained password policies | Windows Server 2012 R2, 2012, 2008 R2, 2008 |
| **Windows Server 2008 R2** | - Authentication mechanism assurance
- Managed Service Accounts | Windows Server 2012 R2, 2012, 2008 R2 |
| **Windows Server 2012** | - KDC support for claims
- Compound authentication
- Kerberos armoring | Windows Server 2012 R2, 2012 |
| **Windows Server 2012 R2** | - Protected Users group enhancements
- Authentication Policies
- Authentication Policy Silos | Windows Server 2012 R2 |
| **Windows Server 2016** | - Smart card required for interactive logon
- Enhanced Kerberos features
- New credential protection features | Windows Server 2019, 2016 |

Forest functional levels have introduced a few key capabilities over the years:

| **Version** | **Capabilities** |
| --- | --- |
| **Windows Server 2003** | Introduction of forest trust, domain renaming, and Read-Only Domain Controllers (RODC). |
| **Windows Server 2008** | All new domains default to the Server 2008 domain functional level. No additional new forest-level features. |
| **Windows Server 2008 R2** | Active Directory Recycle Bin allows restoring deleted objects when AD DS is running. |
| **Windows Server 2012** | All new domains default to Server 2012 domain functional level. No additional new forest-level features. |
| **Windows Server 2012 R2** | All new domains default to Server 2012 R2 domain functional level. No additional new forest-level features. |
| **Windows Server 2016** | Privileged Access Management (PAM) via Microsoft Identity Manager (MIM). |

## Trust

- A trust is used to establish forest-forest or domain-domain authentication, allowing users to access resources in (or administer) another domain outside of the domain their account resides in.
- A trust creates a link between the authentication systems of two domains.

| **Trust Type** | **Description** |
| --- | --- |
| **Parent-child** | Domains within the same forest. The child domain has a two-way transitive trust with the parent domain. |
| **Cross-link** | A trust between child domains (in different trees or branches) within the same forest to optimize and speed up authentication paths. |
| **External** | A non-transitive trust between two separate domains in different forests that are not already joined by a forest trust. Uses SID filtering. |
| **Tree-root** | A two-way transitive trust between a forest root domain and a new tree root domain created within the same forest. Established during domain setup. |
| **Forest** | A transitive trust between the root domains of two separate forests, allowing access across all domains in both forests. |

### Trust Example

![alt text](<Active Directory Functionality/image.png>)

**Trusts** help different domains or forests in a network allow users to access resources from each other.

- **Transitive trust**: Trust passes along. If Domain A trusts Domain B, and Domain B trusts Domain C, then Domain A also trusts Domain C.
- **Non-transitive trust**: Trust does **not** pass along. Domain A only trusts Domain B, but not who Domain B trusts.

**Trusts can also be:**

- **Two-way (bidirectional)**: Both domains trust each other. Users from both sides can access each other's resources.
- **One-way**: Only one domain trusts the other. Only users from the trusted domain can access the trusting domain's resources.

**note**

- Sometimes trusts are set up carelessly, which may open up **security risks**.
- Companies that merge or acquire others might unintentionally allow **too much access** between networks.
- Hackers can use these poorly set-up trusts to steal credentials or gain admin access in the main domain.