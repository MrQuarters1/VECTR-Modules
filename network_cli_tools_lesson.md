---
title: "Network CLI Tools for Troubleshooting"
id: "network-cli-tools-troubleshooting"
author: "Ahmad Hasan"
date: "2026-03-24"
version: "1.0"
---

## Learning Objectives
- Use `ipconfig` and `ifconfig` to inspect host network configuration.
- Use `ping` to test basic reachability and identify simple connectivity failures.
- Use `traceroute` or `tracert` to identify where traffic stops along a path.
- Use `nslookup` and `dig` to verify DNS resolution.
- Use `netstat` to inspect active connections and listening ports.
- Apply these tools together to troubleshoot networking issues in an isolated lab.

## Prerequisites
- Basic familiarity with a terminal
- Basic understanding of IP addresses, subnets, and DNS

## Lab Environment Setup
Kali Base
```bash
RUN sudo apt-get update
RUN sudo apt-get install net-tools -y
RUN sudo apt-get install iputils-ping -y
RUN sudo apt-get install traceroute -y
RUN sudo apt-get install dnsutils -y
```

Windows Base
- Windows 11 VM with Command Prompt or PowerShell available

## Background
This lab supports the NEST Capstone project in the NebraskaCyber MATRIX VECTR environment. The project is focused on building hands-on networking modules in an isolated sandbox using Windows and Kali Linux virtual machines. The purpose of this lesson is to give learners the core command-line tools needed to diagnose broken networking scenarios before moving into more advanced topics such as firewall rules, segmentation, reverse proxies, Docker or Kubernetes networking, and exposed services.

These tools are foundational because they let students answer simple but important troubleshooting questions:
- Does this machine have a valid IP address?
- Can it reach another host?
- Where does the path fail?
- Is DNS working?
- What connections and ports are active on the host?

## Assessment
### Assessment 1
- Run `ipconfig` or `ifconfig`
- Identify the IP address, subnet mask, and default gateway

### Assessment 2
- Run `ping`
- Confirm whether a target is reachable

### Assessment 3
- Run `traceroute` or `tracert`
- Identify where packet forwarding stops

### Assessment 4
- Run `nslookup` and `dig`
- Verify hostname resolution

### Assessment 5
- Run `netstat`
- Identify a listening service or active connection

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

## Step 3: Trace the Path with Traceroute or Tracert
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

## Step 4: Verify DNS Resolution with Nslookup and Dig
A service may work by IP address but fail by hostname. That usually points to DNS.

### Query a hostname with nslookup
```bash
nslookup example.com
```

### Query a hostname with dig
```bash
dig example.com
```

### Query a specific DNS server
```bash
dig @8.8.8.8 example.com
```

Compare:
- Whether the hostname resolves
- Which IP address is returned
- Which DNS server answered
- Whether the response changes between servers

If a website works by IP but not by name, the likely issue is DNS rather than routing or host availability.

## Step 5: Inspect Connections and Ports with Netstat
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

## Step 6: Apply the Full Troubleshooting Process
Use the following order when diagnosing a broken service in the sandbox:

1. Check local configuration with `ipconfig` or `ifconfig`
2. Test reachability with `ping`
3. Identify the traffic path with `traceroute` or `tracert`
4. Confirm name resolution with `nslookup` or `dig`
5. Verify local services and connections with `netstat`

This workflow gives a structured method for diagnosing connectivity, DNS, and service-level failures inside the lab.

## Challenge Task
A web application in the sandbox is unreachable by hostname.

Use the CLI tools in this lesson to answer the following:
- Does the host have a valid local IP configuration?
- Can the target server be reached by IP address?
- Does the route stop at a particular hop?
- Does the hostname resolve correctly?
- Is the expected service listening on the destination host?

Document your commands, findings, and final diagnosis.

## FAQs

### Why use both `nslookup` and `dig`?
Both query DNS, but `dig` provides more detailed output that is useful for troubleshooting and validation.

### Why might `ping` fail even if a host is online?
Some systems or firewall rules block ICMP traffic, so ping failure does not always mean the host is down.

### Why do we use these tools before firewall or proxy troubleshooting?
These commands establish the basic network state first. They help separate simple host or DNS issues from higher-level configuration problems.

## Related Skills & Roles
- Network Administrator
- Cybersecurity Analyst
- Cybersecurity Engineer
- SOC Analyst
- Penetration Tester
