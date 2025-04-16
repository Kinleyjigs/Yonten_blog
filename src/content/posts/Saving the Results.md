---
title: Saving the Results
published: 2025-04-16
description: "How to save Nmap results?"
image: "../../assets/images/nmap/nmap.png"
tags: ["Scan", "Learning"]
category: Nmap
draft: false
---
# Saving the Results

## Different Formats

Nmap can save the results in 3 different formats.

- Normal output (-oN) with the .nmap file extension
- Grepable output (-oG) with the .gnmap file extension
- XML output (-oX) with the .xml file extension

```markdown
sudo nmap 10.10.10.63 -p- -oA target
```

![alt text](<../../assets/images/nmap/Saving the Results/image.png>)

![alt text](<../../assets/images/nmap/Saving the Results/image 1.png>)

### target.gnmap Output (normal output)

![alt text](<../../assets/images/nmap/Saving the Results/image 2.png>)

### target.nmap Output(Grepable Output)

![alt text](<../../assets/images/nmap/Saving the Results/image 3.png>)

### target.xml Output (XML Output)

![alt text](<../../assets/images/nmap/Saving the Results/image 4.png>)

## Style sheets

With the XML output, we can easily create HTML reports that are easy to read, even for non-technical people. This is later very useful for documentation, as it presents our results in a detailed and clear way. To convert the stored results from XML format to HTML, we can use the
tool xsltproc.

```markdown
xsltproc target.xml -o target.html
```

![alt text](<../../assets/images/nmap/Saving the Results/image 5.png>)

### Nmap Report

![alt text](<../../assets/images/nmap/Saving the Results/image 6.png>)