---
title: "Path Analysis and Connection Visibility"
id: "path-analysis-and-connection-visibility"
author: "Ahmad Hasan"
date: "2026-03-24"
version: "1.0"
---

## Learning Objectives
- Use **traceroute** and **tracert** to inspect how traffic moves through the network.
- Use **netstat** to inspect active connections and listening ports.
- Identify whether a problem is caused by path failure, segmentation, or a host-level service issue.

## Prerequisites
- none

## Lab Environment Setup
Kali Base
```bash
RUN sudo apt-get install traceroute -y
RUN sudo apt-get install net-tools -y
```

Windows Base
- Windows 11 VM with Command Prompt or PowerShell available

## Assessment
### Assessment 1:
- Run `traceroute` or `tracert`
- Identify the last successful hop

### Assessment 2
- Run `netstat`
- Identify a listening port or active connection

### Assessment 3
- Use the results to explain whether a problem is caused by routing, segmentation, or service exposure

## FAQs

### What is the difference between `traceroute` and `tracert`?
They provide the same type of path analysis on different operating systems.

### Why is `netstat` useful in security work?
It can reveal open ports, active connections, and potentially suspicious activity.

## Related Skills & Roles
- Network Administrator
- Cybersecurity Analyst
- Cybersecurity Engineer
- Penetration Tester
