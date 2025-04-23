---
title: UTILIZING WHOIS
published: 2025-04-23
description: "Discovering Hidden Information"
image: "../../../assets/images/webinformation/webinfo.jpg"
tags: ["Web information"]
category: Web Information Gathering
draft: false
---
# UTILIZING WHOIS

### **Scenario 1: Spotting a Phishing Scam**

A company’s email security system flags a strange email that was sent to several employees. The email looks like it came from the company’s bank, asking people to click a link and update their account details.

A security analyst checks the link by performing a WHOIS lookup on the domain it points to.

Here’s what they find:

- The domain was registered only a few days ago.
- The registrant’s info is hidden using a privacy service.
- The domain uses name servers from a hosting provider known for allowing shady or criminal activities.

These signs raise serious concern. A newly registered domain, hidden details, and suspicious hosting all point to a phishing attack. The analyst quickly warns the IT team to block the domain and tells staff to avoid the link.

They also start checking the hosting provider to see if the attacker has other phishing domains.

### **Scenario 2: Investigating Malware**

A security researcher is studying a new piece of malware that’s infecting computers in a network. The malware is talking to a remote server (called a command-and-control or C2 server) to get instructions and send out stolen data.

To learn more, the researcher does a WHOIS lookup on the domain the malware connects to.

The WHOIS data shows:

- The domain is registered by someone using a free, anonymous email.
- The location listed is from a country often linked with cybercrime.
- The registrar has a reputation for not dealing well with abuse reports.

These clues suggest the domain is part of a criminal infrastructure, possibly using a "bulletproof" server. The researcher then contacts the hosting provider to report the malicious activity.

### **Scenario 3: Tracking a Cybercriminal Group**

A cybersecurity company is monitoring a well-known hacker group that targets banks. To better understand their operations, analysts collect WHOIS data from domains the group has used in the past.

They find some patterns:

- The domains were often registered around the same time, just before major attacks.
- The names used to register them are fake or aliases.
- Many of the domains share the same name servers, pointing to a shared setup.
- Several domains have already been taken down after past incidents.

Using these patterns, analysts build a clearer picture of how the group operates. They add indicators of compromise (IOCs) to a threat report so other companies can recognize and stop similar attacks in the future.

When performing a WHOIS lookup, we have focus on:

1. **Domain Registration Information:**
    - **Registrar**: Identifies the company that manages the domain registration.
    - **Creation Date**: Shows when the domain was registered, indicating its age and legitimacy.
    - **Expiry Date**: Indicates when the domain will expire. A long validity period suggests stability.
2. **Registrant Information:**
    - **Registrant Organization**: Shows the entity that owns the domain (e.g., Meta Platforms, Inc. for Facebook).
    - **Registrant Contact**: Provides contact details for domain-related issues.
3. **Domain Status:**
    - Look for status codes like **clientDeleteProhibited**, **clientTransferProhibited**, **serverDeleteProhibited**, which indicate protection against unauthorized changes, transfers, or deletions.
4. **Name Servers:**
    - Lists the domain’s DNS servers, which can give insight into the infrastructure and control over the domain.
5. **DNSSEC (Domain Name System Security Extensions):**
    - Indicates if the domain is secured with DNSSEC to protect against domain spoofing.
6. **Last Updated Date:**
    - The last time the WHOIS record was updated, which can help track recent changes.

These details provide essential insights into the domain's ownership, stability, and security measures.