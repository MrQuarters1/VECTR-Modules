--- 
title: "Firewall Management with iptables"
id: "firewall-management-iptables"
author: "Toby Knudsen"
date: "2026-04-07"
version: "1.0"
--- 

## Learning Objectives
- Understand how **iptables** is used for firewall management in Linux
- View and interpret existing iptables rules
- Create basic rules to allow and block traffic
- Test and verify firewall behavior

## Prerequisites
- none


## Lab Environment Setup
Kali Base
```bash
RUN sudo apt-get update -y
RUN sudo apt-get install iptables -y
RUN sudo apt-get install iputils-ping -y
RUN sudo apt-get install net-tools -y
Background Objectives
```

iptables is a legacy firewall tool used in Linux systems to control incoming and outgoing traffic. It works by defining rules that either allow or block packets based on things like IP address, protocol, or port. Even though newer tools like nftables exist, iptables is still widely used and important to understand.

## Step 1: View Current Rules

Check the current iptables rules to see what is already configured.
```bash
sudo iptables -L -v
```
Look at the default chains such as INPUT, OUTPUT, and FORWARD. These control how traffic is handled.

## Step 2: Set Default Policy

Set the default policy for incoming traffic to DROP so that all traffic is blocked unless explicitly allowed.
```bash
sudo iptables -P INPUT DROP
```
Verify the change by running:

sudo iptables -L
### Step 3: Allow Localhost Traffic

Allow traffic from the local machine so basic system processes continue to work.
```bash
sudo iptables -A INPUT -i lo -j ACCEPT
```

### Step 4: Allow Established Connections

Allow responses to outgoing connections so normal browsing and communication works.
```bash
sudo iptables -A INPUT -m conntrack --ctstate ESTABLISHED,RELATED -j ACCEPT
```

### Step 5: Allow ICMP (Ping)

Allow ping requests to test connectivity.
```bash
sudo iptables -A INPUT -p icmp -j ACCEPT
```
Test this by pinging your machine from another system if available.

### Step 6: Block Specific Traffic

Block a specific IP address to simulate restricting access.
```bash
sudo iptables -A INPUT -s 192.168.1.100 -j DROP
```
Replace the IP if needed depending on your environment.

### Step 7: Verify Rules

List all rules again to confirm everything is applied correctly.
```bash
sudo iptables -L -v
```
Make sure your rules appear in the correct order.

### Step 8: Flush Rules (Reset)

Clear all rules to return the system to its original state.
```bash
sudo iptables -F
sudo iptables -P INPUT ACCEPT
```
Verify that rules have been removed:
```bash
sudo iptables -L
```
### Assessment
Assessment 1:
```bash
Run iptables -L -v
```
Identify default chains
Assessment 2:
```bash
Set INPUT policy to DROP
```
Verify change
Assessment 3:
```bash
Add rule to allow localhost traffic
```
Assessment 4:
Add rule for established connections
Confirm connectivity still works
Assessment 5:
Add and test ICMP rule
Assessment 6:
Add a rule to block a specific IP
Assessment 7:
Flush all rules and restore default policy