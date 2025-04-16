---
title: Getting Help
published: 2025-04-16
description: "How to get help in linux"
image: "../../assets/images/linux/linux.png"
tags: ["Linux"]
category: Linux
draft: false
---
# Getting Help

## Getting Help in Linux

- Once you're comfortable with the Linux structure and shell, it's important to know how to get help when using new or unfamiliar commands.

**Common Ways to Get Help:**

1. man pages (Manual Pages):
    - Shows detailed documentation for most commands.
    - Usage: man <command>
    - Example: man ls

1. -help option:
- Displays a quick summary of how to use the command and its options.
- Usage: <command> --help
- Example: ls --help

**Why Use These?**

- Understand a tool before using it.
- Learn available options/flags.
- Discover new tricks or features of common tools.

## First Command:

1. ls command 
- is used to list the files and directories within the current folder or any specified directory.

```markdown
ls
```

![alt text](<../../assets/images/linux/Getting Help 1d7d0918708080afae63f0b586bf2d16/image.png>)

1. man command 
- which displays the manual pages for commands and provides detailed information about their usage.
- **man <tool>**

```markdown
man ls
```

![alt text](<../../assets/images/linux/Getting Help 1d7d0918708080afae63f0b586bf2d16/image 1.png>)

### Syntax:

- <tool> --help

```markdown
ls --help
```

![alt text](<../../assets/images/linux/Getting Help 1d7d0918708080afae63f0b586bf2d16/image 2.png>)

### Syntax:

- <tool> -h

```markdown
curl -h
```

![alt text](<../../assets/images/linux/Getting Help 1d7d0918708080afae63f0b586bf2d16/image 3.png>)

### Syntax:

- apropos <keyword>
- This tool searches the descriptions for instances of a given keyword.

```markdown
apropos sudo
```

![alt text](<../../assets/images/linux/Getting Help 1d7d0918708080afae63f0b586bf2d16/image 4.png>)