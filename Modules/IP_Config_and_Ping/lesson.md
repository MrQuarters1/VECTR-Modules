---
title: "IP Configuration and Basic Reachability"
id: "ip-configuration-and-basic-reachability"
author: "Ahmad Hasan"
date: "2026-03-24"
version: "1.0"
---

## Learning Objectives
- Use **ipconfig** to inspect Windows network configuration.
- Use **ifconfig** to inspect Linux network configuration.
- Use **ping** to test basic reachability.
- Identify common local configuration problems that prevent connectivity.

## Prerequisites
- none

## Lab Environment Setup
Kali Base
```bash
RUN sudo apt-get install net-tools -y
RUN sudo apt-get install iputils-ping -y
```

Windows Base
- Windows 11 VM with Command Prompt or PowerShell available

## Assessment
### Assessment 1:
- Run `ipconfig /all` in Windows
- Identify IP address, subnet mask, default gateway, and DNS server

### Assessment 2
- Run `ifconfig` in Kali
- Identify the active interface and IPv4 address

### Assessment 3
- Run `ping` to test connectivity to localhost and another host

### Assessment 4
- Determine whether a failure is caused by local configuration or simple connectivity loss

## FAQs

### Why do we use both `ipconfig` and `ifconfig`?
They perform similar tasks on different operating systems.

### Why might `ping` fail even if a system is online?
Some systems block ICMP traffic with firewall rules.

## Related Skills & Roles
- Network Administrator
- Cybersecurity Analyst
- Cybersecurity Engineer
- Penetration Tester
