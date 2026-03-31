# Basic Network Segmentation with Subnets

## ID
network-segmentation-subnets  

## Author
Saleh Hayati  

## Date
3/24/2026  

---

## Background Objectives
Network segmentation is used to divide a large network into smaller parts called subnets. This helps improve security and organization. By controlling communication between systems, segmentation prevents attackers from moving freely across the network. Subnets also reduce unnecessary traffic and improve network efficiency.

---

## Step 1: Identify Network Information

Run the following command in Kali:

```bash
ip addr
```

- This command shows your network interface and IP address.

## Reflection Questions:

- What is the IP address of your Kali machine?

---

## Step 2: Test Connectivity

Run the following command in Kali:

```bash
ping 192.168.94.129
```
* This checks if Kali can communicate with the Windows machine.

## Reflection Questions:

- Was the ping successful?

---
## Step 3: Verify Communication

Run the following command in Windows Command Prompt:

```bash
ping 192.168.94.128
```
- This tests communication from Windows to Kali.

## Reflection Questions:

- Can both systems communicate with each other?

---

## Step 4: Apply Network Control

1- Open **Windows Defender Firewall with Advanced Security**.

2- Go to **Inbound Rules**, then disable the following rule:

3- **File and Printer Sharing (Echo Request – ICMPv4-In)**

This blocks ping requests.

## Reflection Questions:
- What happens when ICMP traffic is blocked?

---

## Step 5: Test Segmentation

Run the following command again in Kali:

```bash
ping 192.168.94.129
```
- This tests connectivity after applying firewall restrictions.

## Reflection Questions:

- What happens after blocking ICMP traffic?

---

## Step 6: Analyze Results

After blocking the firewall rule, ping should fail and show **100% packet loss**.

This demonstrates how communication between systems can be restricted.

## Reflection Questions:
- How does blocking traffic **improve** network security?

---

## Learning Objectives

- Understand basic network segmentation using subnets.
- Identify IP addresses using `ip addr`  
- Test connectivity using `ping`  
- Demonstrate how firewall rules control communication 

---

## Prerequisites

- Kali Linux VM  
- Windows VM  
- Basic networking knowledge  

---

## Lab Environment Setup

Kali Base:

```bash
RUN sudo apt-get install iputils-ping -y
