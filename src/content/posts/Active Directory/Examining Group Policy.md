---
title: Examining Group Policy
published: 2025-04-29
description: "Active Directory"
image: "./Why/image.png"
tags: ["Learning"]
category: Active Directory
draft: false
---

# Examining Group Policy

### **Overview**

- **Group Policy**: A Windows feature for configuring user and computer settings.
- **Scope**: Can be used locally or within a **domain** (Active Directory).
- **Purpose**: Manage settings for OS, users, applications, and security.

### **Importance in Security**

- Crucial for securing an enterprise environment.
- Used in **defense-in-depth** strategies.
- Active Directory isn’t secure by default—Group Policy enhances its security posture.

### **Security Risks**

- **Attackers** can abuse Group Policy:
    - Gain rights over Group Policy Objects (GPOs)
    - Perform **lateral movement**, **privilege escalation**, or **domain compromise**
    - Maintain **persistence** in networks
- Understanding GPOs helps in identifying misconfigurations during **penetration testing**.

### **Group Policy Objects (GPOs)**

### **Definition**

- A **GPO** is a set of policy settings applied to users or computers.
- Contains configuration for:
    - Security settings
    - Software installations
    - Application restrictions
    - Network policies, etc.

### **Properties**

- Each GPO has:
    - A **unique name**
    - A **GUID (Globally Unique Identifier)**
- Can be **linked** to:
    - **Organizational Units (OUs)**
    - **Domains**
    - **Sites**
- Multiple GPOs can be applied to the same container.

### **Scope of Application**

- Applied to:
    - **Users**
    - **Groups**
    - **Computers**
- Managed at local machine level or Active Directory level.

### **Examples of GPO Usage**

- Set different **password policies** for different account types.
- **Disable USB ports** or **removable media**.
- Enforce **screensaver with password**.
- Block access to **cmd.exe**, **PowerShell**, or unauthorized applications.
- Enforce **audit and logging** policies.
- Restrict **software installations** and deploy approved software.
- Display **logon banners**.
- Disable **LM hash** usage.
- Run scripts on **startup/shutdown** or **logon/logoff**.

### **Password Policy Example (Windows Server 2008)**

- Enforced by default:
    - **Minimum length**: 7 characters
    - Must include characters from **3 of the following 4** categories:
        - Uppercase (A–Z)
        - Lowercase (a–z)
        - Numbers (0–9)
        - Special characters (e.g., **!@#$%^&*()**)

## Group Policy Order of Precedence (Highest to Lowest)

| **Level** | **Description** |
| --- | --- |
| **Organizational Unit (OU) – Nested** | Settings for **nested OUs** override those in parent OUs. Useful for applying more specific rules, e.g., separate **Applocker policies** for Security Analysts. |
| **Organizational Unit (OU)** | Applies to users/computers in a specific OU. Ideal for **role-based** configurations (e.g., HR access to shared drives, IT access to PowerShell). |
| **Domain-wide Policy** | Applies **across the entire domain**. Common for global settings like password policy, desktop backgrounds, and login banners. |
| **Site Policy** | Applies to a **specific site** in an enterprise. Useful when different physical locations need unique settings (e.g., stricter access control in research buildings). |
| **Local Group Policy** | Set **locally on a host**. Lowest precedence—overwritten by any conflicting higher-level policy. |

## **Group Policy Objects (GPOs): Order of Precedence & Behavior**

[text](<Examining Group Policy>)

### **GPO Processing Order (Precedence)**

- GPOs are processed **top-down** in Active Directory, meaning:
    - **Site-level GPOs → Domain-level GPOs → OU-level GPOs → Child OU GPOs**.
    - The **last applied GPO** takes precedence — it can **override previous GPOs** if settings conflict.
- **Key Rule**:
    
    > GPOs linked directly to Organizational Units (OUs) are processed last, thus have higher precedence than domain- or site-level GPOs.
    > 

### **Link Order Within the Same OU**

- Multiple GPOs can be linked to a single OU.
- These GPOs are processed in the order defined in the **Link Order** list.
    - The GPO with **Link Order 1** is applied **last** and has the **highest precedence**.
    - Example: If “Disallow LM Hash” is Link Order 1, and “Block Removable Media” is Link Order 2 → the **Disallow LM Hash** GPO overrides the others.

### **Enforced GPOs (No Override)**

- When **Enforced** is applied to a GPO:
    - Its settings **cannot be overridden** by GPOs linked to **lower-level OUs**.
    - Used for **critical policies** like **legal login banners**, **password complexity**, etc.
- Formerly known as "**No Override**."
- **Example**:
    - If the **Logon Banner GPO** is enforced at the domain level, it overrides any conflicting settings in all lower OUs.

> ⚠️ If the Default Domain Policy is enforced, it will override all GPOs at all levels, including OU-level policies.
> 

### **Block Inheritance**

- Block Inheritance prevents **GPOs from higher levels** (e.g., domain or parent OU) from applying to a specific OU.
- Common for isolating sensitive or unique environments.
- ⚠️ However, **Enforced GPOs override Block Inheritance**.
    - **Enforced > Block Inheritance**.

## 🔁 **Group Policy Refresh Frequency**

- **Default refresh interval**:
    - **Users/Computers**: every **90 minutes** (±30 min random offset to prevent overload).
    - **Domain Controllers**: every **5 minutes**.
- **Manual refresh**:
    - Use `gpupdate /force` to apply GPOs immediately.
- **Customizing Refresh Interval**:
    - Navigate to:
        
        ```
        pgsql
        CopyEdit
        Computer Configuration →
        Policies →
        Administrative Templates →
        System →
        Group Policy →
        Set Group Policy refresh interval for computers
        
        ```
        
    - ⚠️ Setting too short a refresh interval may cause **network congestion** or **replication issues**.

---

## **Security Considerations with GPOs**

- Misconfigured or overly permissive GPOs can be exploited:
    - Adding **unauthorized local admins**
    - Running **malicious tasks**
    - Establishing **reverse shells**
    - Modifying **group memberships**
- Example of GPO-based attack:
    - Using **BloodHound**, attackers find they can modify the **Disconnect Idle RDP GPO** due to group nesting.
    - If this GPO applies to high-value users (admins), attackers can escalate privileges and move laterally in the domain.
- **Best practices**:
    - Restrict who can modify GPOs.
    - Regularly audit GPO permissions.
    - Monitor for unauthorized changes.

---

## Summary Table: GPO Behavior and Settings

| Feature | Description |
| --- | --- |
| **Processing Order** | GPOs applied last (e.g., at OU level) override earlier ones. |
| **Link Order** | Lower number (e.g., 1) = higher precedence within an OU. |
| **Enforced** | Prevents lower-level OUs from overriding the GPO. |
| **Block Inheritance** | Prevents higher-level GPOs from applying to an OU. |
| **Refresh Interval** | Default: 90 min ± 30 min (users), 5 min (DCs). |
| **Manual Refresh** | Use `gpupdate /force` for immediate update. |
| **Security Risks** | GPOs can be weaponized if misconfigured or poorly secured. |