---
title: IPMI (Intelligent Platform Management Interface)
published: 2025-04-23
description: "What is IPMI?"
image: "../../../assets/images/footprinting/footprinting.jpg"
tags: ["footprinting"]
category: Footprinting
draft: false
---
# IPMI (Intelligent Platform Management Interface)

### 🔍 What is IPMI?

**IPMI** is a **standardized hardware-based system management interface** used for remote monitoring and administration of servers. It operates independently of the host's CPU, OS, BIOS, and firmware, enabling sysadmins to manage systems—even when they're powered off or unresponsive.

> Introduced by: Intel in 1998
> 
> 
> **Commonly found on**: HP iLO, Dell DRAC, Supermicro IPMI
> 
> **Default Port**: **`623/UDP`**
> 

### 💡 Use Cases for IPMI

IPMI is essential in various system states:

- 🧬 **Before OS boots**: Modify BIOS settings remotely
- 📴 **Powered down hosts**: Still accessible for remote power on/off
- ⚠️ **Post-system failure**: Diagnose issues without OS access

Also used to:

- Monitor system **temperature, voltage, fans, power**
- Review **hardware logs** and **inventory**
- Send alerts via **SNMP**

### 🔧 Key IPMI Components

| Component | Function |
| --- | --- |
| **BMC** (Baseboard Management Controller) | Embedded microcontroller that runs IPMI |
| **ICMB** | Interface for inter-chassis communication |
| **IPMB** | Internal bus that connects IPMI components |
| **IPMI Memory** | Stores logs and configuration data |
| **Comm Interfaces** | Serial, LAN, PCI Mgmt, ICMB |

### 🕵️‍♂️ Footprinting IPMI with Nmap

```markdown
sudo nmap -sU --script ipmi-version -p 623 <target>
```

### 🔍 Metasploit: IPMI Version Scan

```markdown
use auxiliary/scanner/ipmi/ipmi_version
set rhosts <target>
set rport 623
run
```

✅ This reveals the **IPMI version** and authentication details.

### 🔑 Default Credentials to Test

| Product | Username | Password |
| --- | --- | --- |
| **Dell iDRAC** | `root` | `calvin` |
| **HP iLO** | `Administrator` | Randomized 8-char (A-Z, 0-9) |
| **Supermicro** | `ADMIN` | `ADMIN` |

### 🧨 Dangerous Vulnerability: RAKP Hash Disclosure

IPMI v2.0 has a flaw where the **server sends a SHA1/MD5 hash before authentication**. This hash can be:

- Extracted and cracked offline
- Used to access BMC
- **Exploited using Hashcat**:

```markdown
hashcat -m 7300 ipmi.txt -a 3 ?1?1?1?1?1?1?1?1 -1 ?d?u
```

🔓 Example: Cracks 8-char uppercase+number password.

### 🪓 Dumping Hashes with Metasploit

```markdown
use auxiliary/scanner/ipmi/ipmi_dumphashes
set rhosts <target>
set rport 623
run
```

### 🔁 Why This Matters

Gaining BMC access = **physical access** to the host:

- Reboot / shutdown systems
- Reinstall OS remotely
- Access serial console or web UI

🧠 **Tip**: Always test **password reuse** once an IPMI credential is cracked.

### ⚠️ Mitigations

- Change default IPMI credentials immediately
- Disable IPMI if not in use
- Use strong, non-reusable passwords
- Apply **network segmentation** to isolate BMC interfaces
- Monitor IPMI traffic on port 623/UDP

### 🧪 Final Thoughts

IPMI is powerful, but risky. It's often overlooked during internal pentests—**don’t make that mistake**. A single exposed BMC could compromise your entire infrastructure.