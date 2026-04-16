---
title: "IP Configuration and Basic Reachability"
id: "ip-configuration-and-basic-reachability"
author: "Ahmad Hasan"
date: "2026-03-24"
version: "1.0"
---

## Learning Objectives
- Use `ipconfig` and `ifconfig` to inspect host network configuration.
- Use `ping` to test basic reachability and identify simple connectivity failures.
- Apply these tools together to troubleshoot basic networking issues in an isolated lab.

## Prerequisites
- Basic familiarity with a terminal
- Basic understanding of IP addresses, subnets, and DNS

## Lab Environment Setup
Kali Base
```bash
RUN sudo apt-get update
RUN sudo apt-get install net-tools -y
RUN sudo apt-get install iputils-ping -y
```

Windows Base
- Windows 11 VM with Command Prompt or PowerShell available

## Background
This lab supports the NEST Capstone project in the NebraskaCyber MATRIX VECTR environment. The project is focused on building hands-on networking modules in an isolated sandbox using Windows and Kali Linux virtual machines. The purpose of this lesson is to give learners the first commands they should use when diagnosing broken networking scenarios.

These tools are foundational because they let students answer simple but important troubleshooting questions:
- Does this machine have a valid IP address?
- Does it have the correct subnet mask and default gateway?
- Can it reach another host on the network?

## Assessment
### Assessment 1
- Run `ipconfig` or `ifconfig`
- Identify the IP address, subnet mask, and default gateway

### Assessment 2
- Run `ping`
- Confirm whether a target is reachable

### Assessment 3
- Use `ipconfig`, `ifconfig`, and `ping` together
- Diagnose whether a problem is caused by bad local configuration or loss of connectivity

## Step 1: Inspect Local Network Configuration
Before testing connectivity, inspect the local network settings of the host.

### On Kali Linux
```bash
ifconfig
```

### On Windows
```powershell
ipconfig /all
```

Review the following values:
- IP address
- Subnet mask
- Default gateway
- DNS server
- Network interface name

If your address, subnet, or gateway is incorrect, the rest of your troubleshooting will likely fail.

## Step 2: Test Basic Reachability with Ping
Use `ping` to determine whether another host is reachable.

### Ping the local host
```bash
ping -c 4 127.0.0.1
```

### Ping another internal host
```bash
ping -c 4 <target_ip>
```

### Windows example
```powershell
ping <target_ip>
```

Use the output to identify:
- Whether the host responds
- Approximate latency
- Packet loss
- Whether the failure appears local or remote

A successful ping means the host is reachable over the network. A failed ping may indicate a firewall rule, routing issue, incorrect IP configuration, or a host that is offline.

## Step 3: Apply the Troubleshooting Process
Use the following order when diagnosing a basic connectivity problem in the sandbox:

1. Check local configuration with `ipconfig` or `ifconfig`
2. Verify the IP address, subnet mask, and default gateway
3. Test reachability with `ping`
4. Decide whether the failure is caused by local configuration or network connectivity

This workflow gives a structured method for diagnosing the first layer of networking problems inside the lab.

## Challenge Task
A system in the sandbox cannot reach an internal server.

Use the CLI tools in this lesson to answer the following:
- Does the host have a valid local IP configuration?
- Is the subnet mask correct?
- Is the default gateway configured?
- Can the target server be reached by IP address?

Document your commands, findings, and final diagnosis.

## FAQs

### Why use both `ipconfig` and `ifconfig`?
They serve similar purposes on different operating systems. `ipconfig` is used on Windows, while `ifconfig` is used on Linux.

### Why might `ping` fail even if a host is online?
Some systems or firewall rules block ICMP traffic, so ping failure does not always mean the host is down.

### Why start with these tools?
These commands establish the basic network state first. They help identify whether the problem begins with local host configuration or simple connectivity failure.

## Related Skills & Roles
- Network Administrator
- Cybersecurity Analyst
- Cybersecurity Engineer
- SOC Analyst
- Penetration Tester
