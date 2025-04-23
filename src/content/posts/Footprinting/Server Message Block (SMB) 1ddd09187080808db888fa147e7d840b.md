---
title: Server Message Block (SMB)
published: 2025-04-23
description: "SMB"
image: "../../../assets/images/footprinting/footprinting.jpg"
tags: ["footprinting"]
category: Footprinting
draft: false
---
# Server Message Block (SMB)

## 🔹 Overview

- **SMB (Server Message Block)** is a client-server protocol for accessing:
    - Files and directories
    - Printers and other shared network resources
- Enables **inter-process communication** over a network.
- Initially popularized via **OS/2 LAN Manager** and later widely used in **Microsoft Windows**.
- **Backward compatibility** in Windows allows newer systems to communicate with older ones.

## 🔹 Key Features
Enables file/service access over the network between SMB-enabled systems.

Uses TCP/IP for transport (typically over port 445).

Access is managed using Access Control Lists (ACLs) with permissions like:

read, write, execute, full control

## 🐧 Samba (SMB on Unix/Linux)

Samba is an open-source SMB server for Linux/Unix.

Implements CIFS (Common Internet File System), a dialect of SMB.

Enables cross-platform communication with Windows systems.

Provides:

SMB file/print sharing

Active Directory integration

### 🔹 Samba Daemons

| Daemon | Role |
| --- | --- |
| `smbd` | Handles SMB protocol and file sharing |
| `nmbd` | Handles NetBIOS name resolution |
| `winbindd` | Manages user/group info from AD |
| `samba` | Manages AD DC (in Samba 4) |

### 📶 SMB Versions

| SMB Version | OS Support | Key Features |
| --- | --- | --- |
| **CIFS** | Windows NT 4.0 | Uses NetBIOS |
| **SMB 1.0** | Windows 2000 | TCP-based |
| **SMB 2.0** | Vista / Server 2008 | Performance, caching |
| **SMB 2.1** | Win 7 / Server 2008 R2 | Locking |
| **SMB 3.0** | Win 8 / Server 2012 | Multichannel, encryption |
| **SMB 3.1.1** | Win 10 / Server 2016 | AES-128, integrity check |

### 🔐 **Important Configuration Options**

| Option | Description |
| --- | --- |
| `workgroup` | Name of SMB workgroup/domain |
| `path` | Directory to share |
| `browseable` | Whether share is visible in network |
| `guest ok` | Allow unauthenticated access |
| `read only` | Prevent modification of files |
| `create mask` | File permission mask |
| `directory mask` | Directory permission mask |
| `map to guest` | Maps unknown users to guest account |

### ⚠️ **Dangerous Settings to Monitor**

| Setting | Risk |
| --- | --- |
| `browseable = yes` | Attackers can enumerate visible shares |
| `read only = no` or `writable = yes` | Allows file creation/modification |
| `guest ok = yes` | Allows anonymous access |
| `create mask = 0777` / `directory mask = 0777` | Full permission to all users |
| `enable privileges = yes` | May allow elevated privileges |
| `magic script` / `logon script` | Risk of executing unauthorized scripts |

### 🌐 **NetBIOS and WINS**

- **NetBIOS**: API for communication over LAN.
- **Name Registration**: Each host registers a unique name.
- **NBNS / WINS**: Servers that resolve NetBIOS names to IPs.