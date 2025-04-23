---
title: Microsoft SQL Server (MSSQL)
published: 2025-04-23
description: "Microsoft SQL Server (MSSQL)"
image: "../../../assets/images/footprinting/window.jpg"
tags: ["footprinting"]
category: Footprinting
draft: false
---
# Microsoft SQL Server (MSSQL)

### **Definition:**

MSSQL is Microsoft’s proprietary relational database management system (RDBMS). Unlike MySQL (which is open-source), MSSQL is closed-source and was initially developed for Windows. However, newer versions can run on Linux and macOS. It's tightly integrated with the .NET Framework, making it popular in enterprise environments.

### 🖥️ **MSSQL Clients**

**Primary Client:**

- **SQL Server Management Studio (SSMS):**
    - GUI-based tool for DB management.
    - Can be installed independently or with MSSQL.
    - May be found with saved credentials on a compromised host.

**Other Useful Clients:**

- `mssql-cli`
- `SQL Server PowerShell`
- `HeidiSQL`
- `SQLPro`
- **`Impacket’s mssqlclient.py`** (commonly used in pentesting)

**🔍 To find Impacket's `mssqlclient.py`:**

```
locate mssqlclient
```

### 📂 **Default MSSQL System Databases**

| Database | Description |
| --- | --- |
| `master` | Tracks all system-level info for an SQL server instance |
| `model` | Template DB for all newly created DBs (changes here apply to new DBs) |
| `msdb` | Used by SQL Server Agent to schedule jobs and alerts |
| `tempdb` | Stores temporary objects |
| `resource` | Read-only DB containing system objects |

### ⚙️ **Default Configuration Highlights**

- SQL Service runs as: `NT SERVICE\MSSQLSERVER`
- **Windows Authentication** is enabled by default.
- **Encryption is not enforced** by default (can be risky).

> 🛡️ Authentication via Windows can involve local SAM or Active Directory.
> 

### ⚠️ **Dangerous or Misconfigured Settings to Look For**

- MSSQL connections **without encryption**
- **Self-signed certificates** (spoofable)
- Use of **Named Pipes**
- **Weak/default `sa` credentials**
- **Overprivileged accounts** via Windows Authentication

---

### 🧭 **Footprinting MSSQL**

### 🔍 Using Nmap

```
sudo nmap -p1433 --script ms-sql-info,ms-sql-empty-password,ms-sql-xp-cmdshell,ms-sql-config 10.129.201.248
```

**Nmap Output Sample:**

- Port: 1433 (open)
- MSSQL Version: SQL Server 2019 RTM
- Named Pipes Enabled: \\target_ip\pipe\sql\query
- Instance: MSSQLSERVER

### 🛠️ Using Metasploit

**Module:** `scanner/mssql/mssql_ping`

```
msf6 > use auxiliary/scanner/mssql/mssql_ping
msf6 auxiliary > set RHOSTS 10.129.201.248
msf6 auxiliary > run
```

### 🔌 **Connecting with `mssqlclient.py`**

If credentials are known, connect via:

```
python3 mssqlclient.py Administrator@10.129.201.248 -windows-auth
```

**Post-connection Output:**

- TLS encryption initiated
- Access to MSSQL CLI using T-SQL

**List Databases:**

```
SQL> select name from sys.databases;
```

**Sample Output:**

```markdown
master
tempdb
model
msdb
```