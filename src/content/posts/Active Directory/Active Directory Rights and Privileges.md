---
title: Active Directory Rights and Privileges
published: 2025-04-29
description: "AD Objects"
image: "./Why/image.png"
tags: ["Learning"]
category: Active Directory
draft: false
---

# Active Directory Rights and Privileges

- Rights and privileges are essential to managing Active Directory (AD), but if they are not handled properly, they can be easily abused by attackers or penetration testers. In AD—and in information security in general—it is important to distinguish between **rights** and **privileges**.
    - **Rights** are permissions that allow a user or group to access specific objects, such as files or folders.
    - **Privileges** allow users to perform specific actions on a system, like shutting it down, running certain programs, or resetting passwords.

- Privileges can be given directly to users or through their membership in certain groups. In Windows, there’s also a system called **User Rights Assignment**. Although it refers to them as “rights,” they are actually privileges granted to users.

## Built-in Active Directory Groups

- Active Directory comes with many built-in security groups. Some of these groups grant powerful rights and privileges that can be used to escalate access within a domain. If not managed carefully, attackers can exploit group memberships to gain control over a domain, even reaching **Domain Admin** or **SYSTEM-level** privileges on a Domain Controller (DC).

Below is a summary of some common built-in AD groups:

| Group Name | Description |
| --- | --- |
| **Account Operators** | Can create and modify most account types (users, local groups, global groups) and log in locally to DCs. Cannot manage key admin accounts. |
| **Administrators** | Have complete control over the computer or entire domain (if on a Domain Controller). |
| **Backup Operators** | Can back up/restore any files, log in/shut down computers, and access critical data like the SAM or NTDS databases. |
| **DnsAdmins** | Can manage DNS settings. This group exists only if a DNS server role was installed on the DC. |
| **Domain Admins** | Have full control of the domain and are local admins on all domain-joined machines. |
| **Domain Computers** | Contains all non-DC computers in the domain. |
| **Domain Controllers** | Contains all Domain Controllers. New DCs are added here automatically. |
| **Domain Guests** | Includes the default Guest account. These users get temporary domain profiles. |
| **Domain Users** | Includes all domain user accounts by default. |
| **Enterprise Admins** | Have full control over the entire AD forest. Can add child domains or create trust relationships. Only exists in the forest root domain. |
| **Event Log Readers** | Can read event logs on local computers. Only exists on promoted domain controllers. |
| **Group Policy Creator Owners** | Can create, edit, and delete Group Policy Objects (GPOs). |
| **Hyper-V Administrators** | Full control over Hyper-V features. Should be treated as Domain Admins if managing virtual DCs. |
| **IIS_IUSRS** | Built-in group used by Internet Information Services (IIS). |
| **Pre–Windows 2000 Compatible Access** | Used for backward compatibility. Often a legacy group that can expose data if not secured. |
| **Print Operators** | Can manage printers on DCs and can escalate privileges by installing malicious drivers. |
| **Protected Users** | Members are protected against credential theft and certain types of attacks. |
| **Read-only Domain Controllers** | Includes all Read-only Domain Controllers in the domain. |
| **Remote Desktop Users** | Allows RDP access to systems. Cannot be deleted or renamed. |
| **Remote Management Users** | Grants access to systems via Windows Remote Management (WinRM). |
| **Schema Admins** | Can change the AD schema (structure of all AD objects). Only exists in the root domain. |
| **Server Operators** | Only on DCs. Can access SMB shares, backup files, and modify services. Default membership is empty. |

### **Example: Server Operators Group Details**

By default, the **Server Operators** group has no members and is set as a **domain local group**. For example:

```sql
PS C:\htb> Get-ADGroup -Identity "Server Operators" -Properties *
```

The output confirms that this group is a critical system object with no members and has the ability to manage domain servers. This group must be managed cautiously.

### **Example: Domain Admins Group Membership**

In contrast, the **Domain Admins** group typically has several members and is a **global group**. These members have full administrative privileges across the domain. For example:

```sql
PS C:\htb> Get-ADGroup -Identity "Domain Admins" -Properties *
```

If any user in this group is compromised, the attacker could gain control of the entire enterprise environment. Therefore, it's critical to monitor and limit who has access to these groups.

### **User Rights Assignment**

Windows allows administrators to assign specific rights to users based on group membership or through **Group Policy Objects (GPOs)**. Not all of these rights are relevant to penetration testers or defenders, but some can lead to serious security risks.

Here are a few important privileges:

| Privilege | Description |
| --- | --- |
| **SeRemoteInteractiveLogonRight** | Allows a user to log in via Remote Desktop (RDP). This can be abused to access systems and escalate privileges. |
| **SeBackupPrivilege** | Lets a user create backups. Can be abused to copy sensitive files like the SAM, SYSTEM, or NTDS.dit for password extraction. |
| **SeDebugPrivilege** | Lets users debug processes. Tools like Mimikatz can use this to read memory and steal credentials from LSASS. |
| **SeImpersonatePrivilege** | Lets users impersonate privileged accounts (like SYSTEM). Can be used with tools like JuicyPotato to gain SYSTEM access. |
| **SeLoadDriverPrivilege** | Lets users load drivers, which can be malicious and lead to system compromise. |
| **SeTakeOwnershipPrivilege** | Lets users take ownership of objects. Can be used to gain unauthorized access to files or resources. |

### Viewing a User's Privileges

To check which privileges a user currently has, use the following command in the Command Prompt or PowerShell:

```bash
whoami /priv
```

**Example Output:**

```sql
PRIVILEGES INFORMATION
----------------------
Privilege Name                    Description                          State
===============================   ================================     ========
SeShutdownPrivilege              Shut down the system                Disabled
SeChangeNotifyPrivilege          Bypass traverse checking             Enabled
SeIncreaseWorkingSetPrivilege    Increase a process working set       Disabled
```

- This helps identify which rights are enabled or disabled for the current user—important for both attackers and defenders during privilege escalation or auditing.