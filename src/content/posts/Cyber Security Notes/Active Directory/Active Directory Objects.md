---
title: Active Directory Objects
published: 2025-04-29
description: "AD Objects"
image: "./Why/image.png"
tags: ["Learning"]
category: Active Directory
draft: false
---

# Active Directory Objects

## AD Objects

![alt text](<Active Directory Objects/image.png>)

## Users

- Users are accounts in Active Directory (AD) used to log in and access resources.
- They are **leaf objects**, meaning they can't contain other objects. Each user has a **Security Identifier (SID)** and **GUID**, and can have many attributes like name, email, login time, manager, etc.
- AD can store over 800 user details, though most environments use only a few. Attackers often target users to gain access to systems.

## **Contacts**

- Contacts represent **external people**, like vendors or customers.
- They also are **leaf objects** but are **not security principals**, meaning they don’t have a SID—just a GUID. They only store info like name, phone number, and email.

## **Printers**

Printer objects represent **network printers**. Like contacts, they are **leaf objects** and not security principals. They have a GUID and details like name, driver, and port.

## **Computers**

- **What are they?**
    
    Any device (workstation or server) that has joined the Active Directory (AD) domain.
    
- **Object type:**
    
    **Leaf object** (cannot contain other objects).
    
- **Security principal:**
    
    ✅ Yes – has both a **SID (Security Identifier)** and **GUID (Globally Unique Identifier)**.
    
- **Importance:**
    - Treated as identities, just like user accounts.
    - Computers can run under **NT AUTHORITY\SYSTEM**, which has high privileges.
    - If an attacker compromises a computer, they may gain access equivalent to a domain user, enabling lateral movement and enumeration of the network.

## **Shared Folders**

- **What are they?**
    
    Objects that point to folders shared on the network from a specific computer.
    
- **Object type:**
    
    **Leaf object**.
    
- **Security principal:**
    
    ❌ No – only has a GUID, not a SID.
    
- **Access control:**
    - Can be **open to all** (even unauthenticated users).
    - **Restricted to authenticated users** (even low-privilege ones).
    - **Locked down** to specific users or groups.
    - Anyone not granted access is denied view or access.
- **Attributes include:**
    - Name
    - System location
    - Access permissions

## **Groups**

- **What are they?**
    
    Objects used to manage multiple users, computers, or other groups.
    
- **Object type:**
    
    **Container object** – can include users, computers, and even other groups.
    
- **Security principal:**
    
    ✅ Yes – has both SID and GUID.
    
- **Purpose:**
    - Simplifies permission management.
    - Example: Assigning a group access to a server means all members inherit access.
- **Nested groups:**
    - Groups inside other groups.
    - Can cause **unintended permissions**.
    - Tools like **BloodHound** help visualize these relationships and potential attack paths.
- **Attributes include:**
    - Group name
    - Description
    - Members
    - Membership in other groups

## **Organizational Units (OUs)**

- **What are they?**
    
    Logical containers used to group similar AD objects (users, groups, computers).
    
- **Object type:**
    
    **Container object**.
    
- **Security principal:**
    
    ❌ No – does **not** have a SID.
    
- **Purpose:**
    - Simplifies **delegation** of administrative tasks.
    - Used for **Group Policy** application across sets of users/computers.
    - Helps structure the AD domain (e.g., Employees > Marketing, HR, etc.).
- **Example use case:**
    
    Assign password reset rights to a Help Desk admin only within a specific OU.
    
- **Attributes include:**
    - Name
    - Members
    - Delegated permissions
    - Linked Group Policies

## **Domain**

- **What is it?**
    
    The **core structure** in Active Directory that holds users, computers, groups, and OUs.
    
- **Each domain has:**
    - Its **own database**.
    - Its **own set of policies** (e.g., default domain password policy).
- **Purpose:**
    - Manages identity, access, and policy enforcement.
    - Policies can include restrictions (like blocking CMD) or mapping network drives.

## **Domain Controllers (DCs)**

- **What are they?**
    
    The **central servers** that run AD services.
    
- **Responsibilities:**
    - Authenticate users and computers.
    - Enforce security policies.
    - Manage and replicate all data in the domain.
- **Importance:**
    - Without DCs, users cannot log in or access resources.
    - Compromising a DC = complete domain control.

## **Sites**

- **What are they?**
    
    Logical groupings of computers and domain controllers **connected via fast networks** (e.g., LAN).
    
- **Purpose:**
    - Optimize **replication** traffic between DCs.
    - Ensure efficient **login and service response** based on physical location.

## **Built-in**

- **What is it?**
    
    A **default container** created when a domain is set up.
    
- **Purpose:**
    
    Holds **predefined security groups** (e.g., Administrators, Users, Guests).
    
- **Note:**
    
    These groups are used for basic permission assignments and role management.
    

## **Foreign Security Principals (FSPs)**

- **What are they?**
    
    Placeholder objects for **external users or groups** from **trusted domains or forests**.
    
- **When are they created?**
    - Automatically, when an **external object** (user, group, computer) is added to a group in the local domain.
- **Attributes:**
    - Hold the **SID** of the external object.
    - Located in the **ForeignSecurityPrincipals** container.
- **Purpose:**
    - Allow cross-domain/forest permissions while maintaining identity.