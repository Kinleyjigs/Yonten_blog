---
title: INTRODUCTION
published: 2025-04-23
description: "Discovering Hidden Information"
image: "../../../assets/images/webinformation/webinfo.jpg"
tags: ["Web information"]
category: Web Information Gathering
draft: false
---
# INTRODUCTION

**Web Reconnaissance:** This is the first phase in a security assessment, where we gather information about target. It is like doing background research, collecting info before attacking. This step helps for further testing and finding potential security issues.

The primary goals of web reconnaissance include:

**Identifying Assets**: it is about finding everything available for public from target. web page, subdomains, IP address and the technology that they use.

**Discovering Hidden Information:** This step involves finding sensitive information that may be accidentally exposed. like backup files and files that contains sensitive info.

**Analyzing the Attack Surface:** This step involves checking the target for possible vulnerabilities. Finding entry point for exploitation.

**Gathering Intelligence:** Gathering information that could help in future attacks. 

# **Types of Reconnaissance**

active and passive 

### **Active Reconnaissance**

- directly interacting with the target system to gather information

| **Technique** | **Description** | **Example** | **Tools** | **Risk of Detection** |
| --- | --- | --- | --- | --- |
| **Port Scanning** | Identifying open ports and services running on the target. | Using Nmap to scan a web server for open ports like 80 (HTTP) and 443 (HTTPS). | Nmap, Masscan, Unicornscan | **High** – Direct interaction may trigger IDS/firewalls. |
| **Vulnerability Scanning** | Probing the target for known vulnerabilities like outdated software or misconfigs. | Running Nessus against a web app to check for SQLi or XSS vulnerabilities. | Nessus, OpenVAS, Nikto | **High** – Exploit payloads are detectable by security tools. |
| **Network Mapping** | Mapping the network topology and connected devices. | Using `traceroute` to identify packet paths and network infrastructure. | Traceroute, Nmap | **Medium to High** – May generate unusual traffic raising suspicion. |
| **Banner Grabbing** | Retrieving banners to identify services and versions. | Connecting to port 80 and examining the HTTP banner for server details. | Netcat, curl | **Low** – Minimal interaction, but may be logged. |
| **OS Fingerprinting** | Identifying the OS of the target system. | Using `nmap -O` to detect whether the target is running Windows, Linux, etc. | Nmap, Xprobe2 | **Low** – Generally passive, but some methods can be detected. |
| **Service Enumeration** | Discovering exact versions of services on open ports. | Using `nmap -sV` to check if a server is running Apache 2.4.50 or Nginx 1.18.0. | Nmap | **Low** – Similar to banner grabbing, usually logged but not alarming. |
| **Web Spidering** | Crawling websites to find directories, files, and hidden resources. | Using Burp Suite Spider or OWASP ZAP Spider to map website structure. | Burp Suite Spider, OWASP ZAP Spider, Scrapy | **Low to Medium** – Can be detected if not mimicking normal user behavior. |

### **Passive Reconnaissance**

- involve gathering info without directly interacting

| **Technique** | **Description** | **Example** | **Tools** | **Risk of Detection** |
| --- | --- | --- | --- | --- |
| **Search Engine Queries** | Using search engines to uncover info about the target (websites, social media, articles). | Searching Google for `"[Target Name]"`. | Google, DuckDuckGo, Bing, Shodan | **Very Low** – Normal internet activity, unlikely to trigger alerts. |
| **WHOIS Lookups** | Query WHOIS databases for domain registration details. | Performing WHOIS lookup to find registrant's name, contact info, and name servers. | `whois` command-line tool, online WHOIS services | **Very Low** – Legitimate queries, no suspicion. |
| **DNS Analysis** | Analyzing DNS records to find subdomains, mail servers, etc. | Using `dig` to enumerate subdomains of a target domain. | `dig`, `nslookup`, `host`, `dnsenum`, `fierce`, `dnsrecon` | **Very Low** – DNS queries are common and typically not flagged. |
| **Web Archive Analysis** | Viewing historical snapshots of websites to identify changes or hidden info. | Using Wayback Machine to view older versions of a target website. | Wayback Machine | **Very Low** – Accessing archived sites is normal behavior. |
| **Social Media Analysis** | Collecting data from social platforms like LinkedIn, Twitter, and Facebook. | Searching LinkedIn for employees to learn roles and identify potential social engineering targets. | LinkedIn, Twitter, Facebook, OSINT tools | **Very Low** – Viewing public profiles isn’t considered intrusive. |
| **Code Repositories** | Searching public code repositories for sensitive info (credentials, vulnerable code). | Searching GitHub for exposed credentials or security flaws in target-related code. | GitHub, GitLab | **Very Low** – Public repositories are intended for open access and searchability. |

Passive reconnaissance is considered more stealthier and provide less info as well.