---
title: "Path Analysis and Connection Visibility"
id: "path-analysis-and-connection-visibility"
author: "Ahmad Hasan"
date: "2026-03-24"
version: "1.0"
---

## Learning Objectives
- Use `traceroute` and `tracert` to identify where traffic stops along a network path.
- Use `netstat` to inspect active connections and listening ports.
- Apply these tools together to troubleshoot routing issues and exposed or active services.

## Prerequisites
- Basic familiarity with a terminal
- Basic understanding of IP addresses, subnets, and routing

## Lab Environment Setup
Kali Base
```bash
RUN sudo apt-get update
RUN sudo apt-get install traceroute -y
RUN sudo apt-get install net-tools -y
```

Windows Base
- Windows 11 VM with Command Prompt or PowerShell available

## Background
This lab supports the NEST Capstone project in the NebraskaCyber MATRIX VECTR environment. The project is focused on building hands-on networking modules in an isolated sandbox using Windows and Kali Linux virtual machines. The purpose of this lesson is to help learners move beyond simple reachability checks and investigate where traffic fails and what network activity is happening on a host.

These tools are important because they let students answer questions such as:
- Where does traffic stop on the network path?
- Is there a bad hop, blocked path, or routing issue?
- What ports are open or listening on the host?
- Are there active or suspicious connections?

## Assessment
### Assessment 1
- Run `traceroute` or `tracert`
- Identify the last successful hop

### Assessment 2
- Run `netstat`
- Identify a listening service or active connection

### Assessment 3
- Use `traceroute`, `tracert`, and `netstat` together
- Diagnose whether a problem is caused by path failure, blocked forwarding, or a service exposure issue

## Step 1: Trace the Path with Traceroute or Tracert
If a host cannot be reached, use `traceroute` or `tracert` to see where traffic stops.

### Kali Linux
```bash
traceroute <target_ip>
```

### Windows
```powershell
tracert <target_ip>
```

Look for:
- The number of hops
- The last successful hop
- Timeouts or unreachable messages

This helps you determine whether the problem is caused by a bad gateway, routing error, segmentation boundary, or blocked hop.

## Step 2: Inspect Connections and Ports with Netstat
Use `netstat` to see which connections are active and which services are listening.

### Kali Linux
```bash
netstat -tunlp
```

### Windows
```powershell
netstat -ano
```

Use the results to identify:
- Listening services
- Open ports
- Established connections
- Suspicious or unexpected network activity

This is especially useful when checking whether a service is actually running and reachable, or when identifying exposed ports in a security-focused troubleshooting scenario.

## Step 3: Apply the Troubleshooting Process
Use the following order when diagnosing a path or service issue in the sandbox:

1. Trace the path with `traceroute` or `tracert`
2. Identify the last successful hop
3. Determine whether the failure points to routing, segmentation, or blocked forwarding
4. Check local services and active connections with `netstat`
5. Verify whether the expected service is listening on the host

This workflow helps separate path-level failures from host-level service issues inside the lab.

## Challenge Task
A service in the sandbox is unreachable from another internal system.

Use the CLI tools in this lesson to answer the following:
- Does the route stop at a particular hop?
- Is there evidence of a routing or segmentation problem?
- Is the expected service listening on the destination host?
- Are there any unexpected open ports or active connections?

Document your commands, findings, and final diagnosis.

## FAQs

### What is the difference between `traceroute` and `tracert`?
They perform the same general function on different operating systems. `traceroute` is commonly used on Linux, while `tracert` is used on Windows.

### Why use `netstat` after `traceroute`?
`traceroute` shows the network path, while `netstat` shows host-level connections and listening services. Together they help determine whether the problem is in transit or on the endpoint.

### Why does this matter for security?
Unexpected listening ports or suspicious active connections may indicate poor service hardening, misconfiguration, or potentially malicious activity.

## Related Skills & Roles
- Network Administrator
- Cybersecurity Analyst
- Cybersecurity Engineer
- SOC Analyst
- Penetration Tester
