---
title: Active Directory Groups
published: 2025-04-29
description: "What Are AD Groups?y"
image: "./Why/image.png"
tags: ["Learning"]
category: Active Directory
draft: false
---

# Active Directory Groups

### **What Are AD Groups?**

- **Groups in Active Directory (AD)** are used to manage permissions for multiple users at once. Instead of assigning rights to each user, admins can assign them to a group.
- It helps to organize users with similar access needs and reduce administrative workload.
- **Groups are important targets for attackers** because poorly configured groups can grant unintended privileges.
- Organizations create both **built-in** and **custom groups**. Without proper checks, the number of groups can grow too much and cause confusion or security risks.
- **Organizational Units (OUs)** are different from groups. OUs are used to organize users, computers, and groups, and apply policies. Groups are mainly used to give access to resources.

### Types of Groups

- **Security Groups** – Used to assign permissions (e.g., access to shared folders or printers). All members inherit the group’s permissions.
- **Distribution Groups** – Used for sending emails to multiple users (e.g., mailing lists in Outlook). They cannot be used to assign access to resources.

### **Group Scopes**

Group scope defines how a group can be used:

1. **Domain Local Group**
    - Used only in the domain where it was created.
    - Can include users from other domains.
    - Can’t be added to global groups.
2. **Global Group**
    - Can access resources in any domain.
    - Can only include users from its own domain.
    - Can be added to other global or local groups.
3. **Universal Group**
    - Used across multiple domains in the same forest.
    - Can contain users or groups from any domain.
    - Stored in the Global Catalog.
    - Changes to universal groups can increase network traffic due to forest-wide replication.

### **Group Scope Conversion Rules**

- A **Global group** can be converted to **Universal**, only if it is not in another global group.
- A **Domain Local group** can be converted to **Universal**, only if it doesn't include other local groups.
- A **Universal group** can become a **Local** group anytime.
- A **Universal group** can become a **Global** group only if it doesn’t include other universal groups

### **Built-in vs. Custom Groups**

- **Built-in groups** (like Domain Admins) are created by default during domain setup and have specific roles.
- **Custom groups** are created by administrators based on organizational needs.
- **Built-in groups** often cannot contain other groups, only user accounts.

### **Nested Groups**

- A **group inside another group** is called a **nested group**.
- Users can inherit permissions indirectly through nested groups.
- This can lead to **unintended access**, so it's important to audit group memberships regularly.
- Tools like **BloodHound** help visualize and track group relationships.

### **Important Group Attributes**

- **cn** – Group’s name.
- **member** – Users or groups inside the group.
- **groupType** – Tells if it's a security or distribution group.
- **memberOf** – Lists the groups that contain this group (nested info).
- **objectSID** – Unique ID of the group.