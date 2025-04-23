---
title: SNMP (Simple Network Management Protocol
published: 2025-04-23
description: "What is SNMP?"
image: "../../../assets/images/footprinting/footprinting.jpg"
tags: ["footprinting"]
category: Footprinting
draft: false
---
# SNMP (Simple Network Management Protocol)

### **What is SNMP?**

SNMP helps monitor and manage devices on a network—like routers, switches, servers, and IoT devices. You can use it to get info from them **or even change settings remotely**.

- It works over **UDP port 161** for sending/receiving data.
- It can also use **UDP port 162** to send **traps** (alerts from device to client without being asked).
- The latest version is **SNMPv3**, which adds **more security** (but also more setup work).

### 🧠 Key Concepts in SNMP

**🔸 MIB (Management Information Base)**

A **dictionary** for SNMP. It lists what data a device has and where to find it.

- Written in a format called **ASN.1** (looks like a tree).
- Includes **OIDs** (Object Identifiers).

**🔸 OID (Object Identifier)**

These are like **addresses** for pieces of information.

- Written in **dot format**, like `1.3.6.1.2.1.1.5.0`
- The longer the OID, the more specific the data.

### 📦 SNMP Versions Overview

| Version | Security | Notes |
| --- | --- | --- |
| **v1** | ❌ None | Basic, still used in small setups. Everything is in **plain text**. |
| **v2c** | ❌ None | Same security as v1 but supports more features. The “c” stands for **community-based**. |
| **v3** | ✅ Strong | Adds **encryption, authentication**, but is more complex to configure. |

### 🔐 Community Strings (like passwords)

- Used to control access.
- If someone knows it (e.g., `public`), they can **read info or even change settings**.
- They're often sent in **plain text**, so attackers can **intercept them** if not secured!

### 🛠️ SNMP Default Config Example

Here’s a cleaned-up config for an SNMP daemon (server):

```
sysLocation Sitting on the Dock of the Bay
sysContact Me <me@example.org>
sysServices 72
master agentx
agentaddress 127.0.0.1,[::1]
view systemonly included .1.3.6.1.2.1.1
rocommunity public default -V systemonly
rocommunity6 public default -V systemonly
rouser authPrivUser authpriv -V systemonly
```

- rocommunity = read-only community string
- view systemonly = restricts which parts of MIB are accessible

### ⚠️ Dangerous Settings to Watch For

| Version | Security | Notes |
| --- | --- | --- |
| **v1** | ❌ None | Basic, still used in small setups. Everything is in **plain text**. |
| **v2c** | ❌ None | Same security as v1 but supports more features. The “c” stands for **community-based**. |
| **v3** | ✅ Strong | Adds **encryption, authentication**, but is more complex to configure. |

### 🔐 Community Strings (like passwords)

- Used to control access.
- If someone knows it (e.g., `public`), they can **read info or even change settings**.
- They're often sent in **plain text**, so attackers can **intercept them** if not secured!

### 🛠️ SNMP Default Config Example

Here’s a cleaned-up config for an SNMP daemon (server):

```
sysLocation Sitting on the Dock of the Bay
sysContact Me <me@example.org>
sysServices 72
master agentx
agentaddress 127.0.0.1,[::1]
view systemonly included .1.3.6.1.2.1.1
rocommunity public default -V systemonly
rocommunity6 public default -V systemonly
rouser authPrivUser authpriv -V systemonly
```

- `rocommunity` = read-only community string
- `view systemonly` = restricts which parts of MIB are accessible

### ⚠️ Dangerous Settings to Watch For

| Setting | Description |
| --- | --- |
| `rwuser noauth` | Full access without login. Very risky! |
| `rwcommunity <string> <IP>` | Full access to everything. |
| `rwcommunity6 <string> <IPv6>` | Same as above but for IPv6. |

### 🕵️ Footprinting SNMP (Info Gathering)

**Tools to use:**

- 🐚 `snmpwalk` – Reads SNMP data from a device.

```
snmpwalk -v2c -c public 10.129.14.128
```

- 🧠 `onesixtyone` – Brute-forces SNMP community strings.
- 🧪 `braa` – Another SNMP scanner.

Example Output from `snmpwalk`:

```
iso.3.6.1.2.1.1.1.0 = "Linux htb ..."
iso.3.6.1.2.1.1.5.0 = "htb"  ← hostname
iso.3.6.1.2.1.1.6.0 = "Sitting on the Dock of the Bay"  ← location
```