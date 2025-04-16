---
title: Host Discovery
published: 2025-04-16
description: "How to Discover Hosts?"
image: "../../assets/images/nmap/nmap.png"
tags: ["Scan", "Learning"]
category: Nmap
draft: false
---
# Host Discovery

### **Why Host Discovery?**

- To identify **which systems are online** in a company's network.
- Helps to know **what machines we can interact with** during the test.

### **How to Discover Hosts**

- Use **Nmap host discovery** options.
- Most effective method is **ICMP Echo Request (Ping)** – checks if the target responds.

## Scan Network Range

```markdown
sudo nmap 10.129.2.0/24 -sn -oA tnet | grep for | cut -d" " -f5
```

![alt text](<../../assets/images/nmap/Host Discovery/image.png>)

![alt text](<../../assets/images/nmap/Host Discovery/image 1.png>)

- This scanning method works only if the firewalls of the hosts allow it. Otherwise, we can use other scanning techniques to find out if the hosts are active or not.

## Scan Single IP

```markdown
sudo nmap 10.129.2.18 -sn -oA host 
```

![alt text](<../../assets/images/nmap/Host Discovery/image 2.png>)

![alt text](<../../assets/images/nmap/Host Discovery/image 3.png>)

## Nmap Ping Scan Behavior (with -sn)

```markdown
sudo nmap 10.10.10.63 -sn -oA host -PE --packet-trace
```

- Using -sn (no port scan), Nmap does a ping scan.
- By default, it sends ICMP Echo Requests (-PE) to check if hosts are alive.
- But on local networks, Nmap sends an ARP ping first.
    - If ARP reply is received, it skips ICMP.
- To force ICMP ping, use the -PE option.
- Use --packet-trace to see exactly what packets are sent.

![alt text](<../../assets/images/nmap/Host Discovery/image 4.png>)

![alt text](<../../assets/images/nmap/Host Discovery/image 5.png>)

## Disabling ARP Ping in Nmap

```markdown
sudo nmap 10.10.10.63 -sn -oA host -PE --packet-trace --disable-arp-ping
```

- Nmap uses ARP requests to check if a host is alive on local networks.
- To skip ARP and use only ICMP echo.
- This forces Nmap to send ICMP Echo Requests instead.
- Use --packet-trace to see the sent/received packets.

![alt text](<../../assets/images/nmap/Host Discovery/image 6.png>)