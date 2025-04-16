---
title: Prompt Description
published: 2025-04-16
description: Understanding and Customizing the Bash Prompt"
image: "../../assets/images/linux/linux.png"
tags: ["Linux"]
category: Linux
draft: false
---
# Prompt Description

## Understanding and Customizing the Bash Prompt

- The Bash prompt appears when the system is ready for a command.
- By default, it shows:

```markdown
<username>@<hostname>:<current directory>$

```

Example: user@kali:~$

**~** refers to the home directory

**$** indicates a regular user

**#**  indicates root user

## **PS1 Variable – Controls Prompt Appearance**

- The **PS1 variable** defines how the prompt looks.
- When not set properly, the prompt may show only $ or **#** without extra info.

### Useful PS1 Special Characters

| Symbol | Description |
| --- | --- |
| `\\u` | Username |
| `\\h` | Hostname (short) |
| `\\H` | Hostname (full) |
| `\\w` | Current working directory (full path) |
| `\\d` | Date (e.g., Mon Feb 6) |
| `\\D{%Y-%m-%d}` | Custom date format (e.g., 2025-04-16) |
| `\\t` | Current time (24-hour) |
| `\\T` | Current time (12-hour) |
| `\\@` | Time (AM/PM) |
| `\\s` | Shell name |
| `\\n` | New line |
| `\\r` | Carriage return |

## Why Customize the Prompt?

- Adds useful info (e.g., time, path, IP).
- Helps in pentesting and troubleshooting.
- Can be made colorful and clean using .bashrc, bash-prompt-generator, or Powerline.