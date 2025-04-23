---
title: Network File System (NFS)
published: 2025-04-23
description: "NFS"
image: "../../../assets/images/footprinting/footprinting.jpg"
tags: ["footprinting"]
category: Footprinting
draft: false
---
# Network File System (NFS)

## 📌 Overview

- **NFS** is developed by **Sun Microsystems** to access files over a network as if they were local.
- Primarily used between **Linux/Unix systems**, unlike **SMB**, which is used by Windows.
- **NFSv3** authenticates the client computer, while **NFSv4** authenticates the user (like SMB).
- Governed by the **Internet standard** for distributed file systems.

## 🔢 NFS Versions & Features

| Version | Features |
| --- | --- |
| **NFSv2** | Old version, supports many systems, uses UDP. |
| **NFSv3** | Supports variable file sizes, better error reporting, backward incompatible with NFSv2. |
| **NFSv4** | Supports Kerberos, firewalls, Internet; adds ACLs, state-based ops, high security. |
| **NFSv4.1** | Adds cluster support, **pNFS**, session trunking (multipathing), and simplifies firewall configs using port **2049 only**. |

## 🔐 Authentication & Authorization

- Based on **ONC-RPC (SUN-RPC)** protocol.
- Uses **XDR** for platform-independent data exchange.
- **Authentication via RPC**, usually through **UID/GID and group memberships**.
- UID/GID mismatch across client and server can lead to access issues.
- Best used in **trusted networks**.

### 📁 Common Options

| Option | Description |
| --- | --- |
| `rw` | Read/write access |
| `ro` | Read-only access |
| `sync` | Synchronous data transfer (safer) |
| `async` | Asynchronous (faster, less safe) |
| `secure` | Uses ports below 1024 |
| `insecure` | Allows ports above 1024 |
| `no_subtree_check` | Disables subtree validation |
| `root_squash` | Maps root UID/GID to anonymous (prevents root access) |

### ⚠️ Dangerous Settings

| Option | Risk |
| --- | --- |
| `rw` | Full access to files |
| `insecure` | Allows user-mode programs to access NFS |
| `nohide` | Exposes sub-mounted filesystems unintentionally |
| `no_root_squash` | Grants root full access — **security risk** |

### 🛠️ Managing Exports

```
# Add entry
echo '/mnt/nfs 10.129.14.0/24(sync,no_subtree_check)' >> /etc/exports

# Restart NFS service
systemctl restart nfs-kernel-server

# View exports
exportfs

```

### 🕵️ Footprinting NFS

### 📌 Important Ports

- **TCP/UDP 111** (rpcbind)
- **TCP/UDP 2049** (nfs)

### 🔍 Nmap Scanning

**Basic scan for services:**

```
sudo nmap 10.129.14.128 -p111,2049 -sV -sC
```

Nmap NSE scripts:

```
sudo nmap --script nfs* 10.129.14.128 -sV -p111,2049
```

**Useful Outputs:**

- List of mounted shares
- File listing (`nfs-ls`)
- Share details (`nfs-showmount`)
- Filesystem stats (`nfs-statfs`)
- Running RPC services (`rpcinfo`)

### 🧪 Practical Tips

- Create different folders with various settings to test NFS permissions and enumeration.
- Pay attention to port configurations and **root access options**.
- Use **Nmap scripts** for detailed service analysis.