---
title: "DNS Resolution"
id: "dns-resolution"
author: "Ahmad Hasan"
date: "2026-03-24"
version: "1.0"
---

## Learning Objectives
- Use **nslookup** to perform basic DNS lookups.
- Use **dig** to inspect DNS responses in more detail.
- Identify when a connectivity problem is actually caused by DNS.

## Prerequisites
- none

## Lab Environment Setup
Kali Base
```bash
RUN sudo apt-get install dnsutils -y
```

Windows Base
- Windows 11 VM with Command Prompt or PowerShell available
- `nslookup` available by default

## Assessment
### Assessment 1:
- Run `nslookup`
- Identify the returned IP address and responding DNS server

### Assessment 2
- Run `dig`
- Identify the answer section and query status

### Assessment 3
- Explain whether a failure is caused by incorrect or missing DNS resolution

## FAQs

### Why use both `nslookup` and `dig`?
`nslookup` is simple and readable, while `dig` provides more detailed DNS output.

### Why separate DNS from basic connectivity?
A service may work by IP address but fail by hostname, which usually points to a DNS issue.

## Related Skills & Roles
- Network Administrator
- Cybersecurity Analyst
- Cybersecurity Engineer
- Penetration Tester
