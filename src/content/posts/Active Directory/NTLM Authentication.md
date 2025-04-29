---
title: NTLM Authentication
published: 2025-04-29
description: "NTLM Authentication"
image: "./Why/image.png"
tags: ["Learning"]
category: Active Directory
draft: false
---

# NTLM Authentication

## Overview

NTLM (NT LAN Manager) is a family of authentication protocols used by Microsoft Windows systems. These protocols were predecessors to Kerberos and are still present in various legacy systems and applications.

NTLM uses cryptographic hash functions and challenge-response mechanisms for authentication. Despite being deprecated in favor of Kerberos, NTLM (especially NTLMv2) is still widely encountered in enterprise environments.

## Core Concepts

### Hashes vs Protocols

- **LM and NTLM**: Refers to the *hash types* used for storing passwords.
- **NTLMv1 and NTLMv2**: Refers to *authentication protocols* that utilize these hashes.
- **Kerberos**: More secure protocol using tickets and mutual authentication.

| Protocol | Cryptography | Mutual Auth | Auth Message | Trusted Third Party |
| --- | --- | --- | --- | --- |
| LM | DES | ❌ | - | Domain Controller |
| NTLM | Symmetric key | ❌ | Random number | Domain Controller |
| NTLMv1 | Symmetric key + MD4 | ❌ | MD4 + Random | Domain Controller |
| NTLMv2 | Symmetric key + HMAC-MD5 | ❌ | HMAC-MD5 + Random | Domain Controller |
| **Kerberos** | Symmetric + Asymmetric | ✅ | Encrypted ticket | Key Distribution Center |

## LAN Manager (LM)

### History & Storage

- Oldest hash system (1987).
- Stored in **SAM** (local) or **NTDS.dit** (domain controller).
- Disabled by default since Windows Vista / Server 2008.

### Security Weaknesses

- Max 14-character passwords.
- Case-insensitive; converted to uppercase.
- Limited keyspace (69 characters).
- Hash split into two 7-character chunks → Easy brute-force using GPU tools like **Hashcat**.
- **Padding** with NULL if password < 14 chars.
- Hash = `DES(KGS!@#$%, 7-char part)` × 2 → then concatenated.

**Example LM Hash:**

```
CopyEdit
299bd128c1101fd6
```

## NT Hash (NTLM)

### Description

- Still used in modern systems.
- Uses MD4 over the UTF-16 LE encoded password.

### NTLM Authentication Flow

1. **NEGOTIATE_MESSAGE** from client.
2. **CHALLENGE_MESSAGE** from server.
3. **AUTHENTICATE_MESSAGE** from client with NT hash.

### Storage

- Stored in **SAM** or **NTDS.dit**.
- Example formula: `MD4(UTF-16-LE(password))`

### Vulnerabilities

- Supports Unicode.
- Crackable via **Hashcat** using GPU.
- Susceptible to **pass-the-hash (PtH)** attacks.
    - No need to know the original password; use NT hash directly.

**NTLM Hash Example:**

```ruby
Rachel:500:aad3c435b514a4eeaad3b935b51304fe:e46b9e548fa0d122de7f59fb6d48eaa2:::
```

### Breakdown:

- `Rachel`: Username
- `500`: RID (Administrator)
- `aad3c...`: LM hash (can be null if disabled)
- `e46b9...`: NT hash (used in PtH)

**PtH Attack Example:**

```ruby
crackmapexec smb 10.129.41.19 -u rachel -H e46b9e548fa0d122de7f59fb6d48eaa2
```

## NTLMv1 (Net-NTLMv1)

### Process

- Uses challenge/response with **NT or LM hash**.
- Weak and deprecated.
- Easy to crack offline using **Responder**, **NTLM Relay**, or **Hashcat**.

### Algorithm

```
C = 8-byte challenge from server
K1 | K2 | K3 = NT/LM Hash + padding
Response = DES(K1, C) + DES(K2, C) + DES(K3, C)
```

**Example NTLMv1 Hash:**

```
u4-netntlm::kNS:338d08f8e26de93300000000000000000000000000000000:9526fb8c23a90751cdd619b6cea564742e1e4bf33
```

## Domain Cached Credentials (MSCache)

### Purpose

- Used when host cannot contact Domain Controller.
- Saves recent credentials for offline logins.

### Storage

- Stores last **10 domain user hashes**.
- Stored in Windows Registry:

```sql
HKEY_LOCAL_MACHINE\SECURITY\Cache
```

### Notes

- Known as **DCC1 (MSCache v1)** and **DCC2 (MSCache v2)**.
- Can be dumped and cracked offline.

### Summary of Attacks & Tools

| Attack Type | Applicable To | Tools |
| --- | --- | --- |
| Brute-force | LM, NTLM | Hashcat |
| Pass-the-Hash (PtH) | NTLM | CrackMapExec, Mimikatz |
| Relay Attacks | NTLMv1/v2 | Responder, NTLMRelayx |
| Credential Dumping | LM/NTLM, DCC | Mimikatz, SecretsDump |
| Offline Cracking | LM, NTLMv1/v2, DCC | John the Ripper, Hashcat |