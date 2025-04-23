---
title: Linux Remote Management Protocols
published: 2025-04-23
description: "SSH (Secure Shell)"
image: "../../../assets/images/footprinting/footprinting.jpg" 
tags: ["footprinting"]
category: Footprinting
draft: false
---
# Linux Remote Management Protocols

In Linux environments, remote management is essential for supporting and troubleshooting systems from different locations. Tools like SSH make it possible to securely access and control remote servers without being physically present. However, misconfigurations can pose serious security risks, making it a vital area of focus for system administrators and penetration testers alike.

### 🔐 **SSH (Secure Shell)**

- **Purpose**: Provides encrypted communication between two systems over TCP port **22**.
- **Cross-Platform**: Available on Linux, macOS (native), and Windows (via tools like PuTTY or OpenSSH).
- **Common Usage**: Remote command execution, file transfer (SCP/SFTP), port forwarding.

### 🔑 **Authentication Methods (OpenSSH supports six)**:

1. Password Authentication
2. **Public-Key Authentication** (most secure & widely used)
3. Host-Based Authentication
4. Keyboard Authentication
5. Challenge-Response Authentication
6. GSSAPI Authentication

### 🧾 **Public-Key Authentication Explained**

- The **private key** stays on the client; the **public key** is stored on the server.
- The client solves a cryptographic challenge from the server using the private key.
- A **passphrase** protects the private key locally.
- Once authenticated, users can access multiple servers without re-entering credentials.

### ⚙️ **Default SSH Configuration** (`/etc/ssh/sshd_config`)

```markdown
Include /etc/ssh/sshd_config.d/*.conf
ChallengeResponseAuthentication no
UsePAM yes
X11Forwarding yes
PrintMotd no
AcceptEnv LANG LC_*
Subsystem sftp /usr/lib/openssh/sftp-server
```

Most options are **commented out** and must be **manually configured**.

### ⚠️ **Dangerous SSH Settings to Avoid**

| Setting | Description |
| --- | --- |
| `PasswordAuthentication yes` | Enables brute-forceable logins |
| `PermitEmptyPasswords yes` | Allows login without a password |
| `PermitRootLogin yes` | Grants root access remotely |
| `Protocol 1` | Uses outdated SSH-1 vulnerable to MITM attacks |
| `X11Forwarding yes` | May enable GUI-based command injection |
| `AllowTcpForwarding yes` | Allows potential data exfiltration |
| `DebianBanner yes` | Exposes system identity |

### 🕵️ **Footprinting with `ssh-audit`**

Tool: [ssh-audit](https://github.com/jtesta/ssh-audit)

```markdown
git clone https://github.com/jtesta/ssh-audit.git && cd ssh-audit
./ssh-audit.py <target-ip>
```

Reveals:

- Banner & version (e.g., OpenSSH_8.2p1)
- Enabled **key exchange algorithms**, some may be **deprecated**
- Supported **authentication methods**
- Weak cryptographic settings (e.g., `ecdsa-sha2-nistp*`, `ssh-rsa`)

### 🔄 **Changing Authentication Preference (Client-side)**

```markdown
ssh -v cry0l1t3@10.129.14.132
```

To brute-force a specific method:

```markdown
ssh -o PreferredAuthentications=password -v cry0l1t3@<target-ip>
```

### 🛡️ **Conclusion**

- SSH is a secure and efficient remote management protocol.
- Misconfiguration can lead to severe vulnerabilities.
- Use tools like `ssh-audit` for hardening your setup.
- Always disable unnecessary authentication methods and deprecated settings.