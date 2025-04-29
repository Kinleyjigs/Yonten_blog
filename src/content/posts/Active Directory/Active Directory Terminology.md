---
title: Active Directory Terminology
published: 2025-04-29
description: "Active Directory"
image: "./Why/image.png"
tags: ["Learning"]
category: Active Directory
draft: false
---

# Active Directory Terminology

### **Object**

- Any resource in AD: users, computers, OUs, printers, domain controllers, etc.

### **Attributes**

- Define properties of an object (e.g., `displayName`, `givenName`).
- Used in **LDAP** queries.

### **Schema**

- The **blueprint** of AD.
- Defines object **classes** (like `user`, `computer`) and their **attributes**.
- When an object is created from a class, it's an **instance** (e.g., `RDS01` is an instance of the `computer` class).

### **Domain**

- A **logical group** of AD objects (users, computers, OUs).
- Can function independently or have **trust relationships** with others.
- Think of it as a **city**.

### **Forest**

- A **collection of domains**.
- Topmost container in AD.
- Think of it as a **state or country**.

### **Tree**

- A group of domains with a shared **root domain**.
- All domains share a **namespace** and **Global Catalog**.
- Trees form **parent-child trust relationships**.

### **Container**

- An object that **holds other objects**.
- Part of the AD hierarchy.

### **Leaf**

- An object that **does not hold** other objects.
- Located at the **end of the hierarchy**.

### **Global Unique Identifier (GUID)**

- A **128-bit unique identifier** for every AD object.
- Stored in `objectGUID` attribute.
- Never changes during the object’s lifetime.
- Used in **precise AD searches**.

### **Security Principals**

- Entities that can be **authenticated**: users, computers, service accounts, etc.
- Used to control access to domain resources.
- **Local accounts** are managed by **SAM**, not AD.

### **Security Identifier (SID)**

- A **unique value** assigned to security principals/groups.
- Issued by the **domain controller**.
- SID is stored in an access token upon login.
- **Well-known SIDs** exist (e.g., `Everyone` group).

### **Distinguished Name (DN)**

- Full path to an object in AD.
- Example:
    
    `cn=bjones,ou=IT,ou=Employees,dc=inlanefreight,dc=local`
    

### **Relative Distinguished Name (RDN)**

- The **unique identifier** at a specific level in the hierarchy.
- Example: `bjones` in `cn=bjones,ou=IT...`.
- Two objects can have the same RDN if they are in different containers.

### sAMAccountName

- This is the **username** used for login (e.g., bjones).
- Must be **unique** and **20 characters or less**.

### userPrincipalName (UPN)

- Another way to log in. Looks like an **email** (e.g., bjones@inlanefreight.local).
- It's optional but helpful in larger networks.

### FSMO Roles (Flexible Single Master Operations)

Active Directory needs **specific roles** to avoid **conflicts and errors** when making changes.

There are **5 FSMO roles**:

1. **Schema Master** – Handles changes to the AD structure (like attributes).
2. **Domain Naming Master** – Manages domain names in the forest.
3. **RID Master** – Gives out unique IDs to objects.
4. **PDC Emulator** – Time sync, password updates, and fallback for older systems.
5. **Infrastructure Master** – Updates references across domains.

💡 All five are assigned to the **first DC (Domain Controller)**. You can later transfer them as needed.

### Global Catalog (GC)

- Stores **all object info** across **all domains** in the forest.
- Used for **logins and searching** for users or resources.

### RODC (Read-Only Domain Controller)

- Like a normal DC, but **read-only**.
- Safer for **remote offices**—can’t change anything.
- No passwords stored (except RODC account and special keys).

### Replication

- Keeps all Domain Controllers **updated**.
- Managed by a built-in service called **KCC**.
- Ensures if one DC fails, others still have the correct data.

### SPN (Service Principal Name)

- A **unique ID for a service**.
- Helps **Kerberos authentication** link a service with a login.

### Group Policy Object (GPO)

- A **collection of rules** to control settings for users/computers.
- Can apply to entire domains or just small groups (OUs).

### ACL (Access Control List)

- A list of **who can access what** and **what they can do**.
- Made up of **ACEs**.

### ACE (Access Control Entry)

- Each ACE says: **who (user/group)** and **what permissions** they have.

### DACL (Discretionary ACL)

- Says **who is allowed or denied** access.
- If missing: **everyone can access**.
- If empty: **no one can access**.

### SACL (System ACL)

- Used for **auditing**.
- Logs **who accessed what and when**.

### FQDN (Fully Qualified Domain Name)

- Full name of a computer or service in a domain (e.g., `DC01.inlanefreight.local`).
- Like a complete web address.

### Tombstone

- When you delete something in AD, it's not gone right away.
- It becomes a **"tombstone"** and stays for 60 or 180 days.
- After that, it’s **permanently deleted** unless you use backups.

### AD Recycle Bin

- Lets admins **restore deleted objects** (like users or groups).
- **Keeps most settings**, unlike tombstones.
- Default restore period: **60 days**.

### SYSVOL

- A shared folder on DCs.
- Stores **scripts, GPO settings**, and **public AD files**.
- Synced to all DCs.

### AdminSDHolder

- Protects **privileged accounts** (like Domain Admins).
- Applies **security settings** to make sure no one can sneak changes.

### dsHeuristics

- Controls extra AD settings across the forest.
- Can be used to **exclude** some groups from AdminSDHolder protection.

### adminCount

- Shows if a user is **protected** by AdminSDHolder.
- `1` = Protected.
- `0` = Not protected.

### ADUC (Active Directory Users and Computers)

- A **GUI tool** to manage users, groups, and computers in AD.
- You can also do the same via **PowerShell**.

### ADSI Edit

- A **powerful tool** to view/edit **deep AD settings**.
- Be careful—**mistakes can break the system**.

### sIDHistory

- Keeps track of **old SIDs** (Security IDs).
- Used in **migrations** so users keep access rights.
- Can be abused if **not secured properly**.

### What You Can Do in Your Assignment:

To complete your **Educare Skill assignment**, you can:

1. **Explain each of these concepts** in your own words (like above).
2. **Create a summary table** or **diagram** of the 5 FSMO roles.
3. Demonstrate understanding with **real-world examples** (e.g., "If a Domain Controller goes offline...").
4. Add **PowerShell examples** or use **ADUC screenshots** if you're doing a practical part.
5. Reflect: **Why are these concepts important for system administrators or cybersecurity?**