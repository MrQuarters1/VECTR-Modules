---
title: "Modernization with nftables"
id: "modernization-with-nftables"
author: "Toby Knudsen"
date: "2026-03-30"
version: "1.3"
---

## Learning Objectives
- Understand how **nftables** modernizes Linux firewall management
- View and interpret an nftables ruleset
- Create tables, chains, and rules
- Test and verify allowed and blocked traffic

## Prerequisites
- none


## Lab Environment Setup
Kali Base
```bash
RUN sudo apt-get update -y
RUN sudo apt-get install nftables -y
RUN sudo apt-get install iputils-ping -y
RUN sudo apt-get install net-tools -y
```

## Background Objectives
nftables is the modern replacement for iptables in Linux systems. Instead of using multiple tools and formats, nftables combines everything into a single framework that uses tables, chains, and rules. This makes firewall management more consistent and easier to understand. In this lab, you will build a basic ruleset from scratch and test how traffic is handled.

## Step 1: Verify nftables Installation
Before starting, confirm nftables is installed.

- In a terminal:
```bash
nft --version
```

- If it is not installed:
```bash
sudo apt-get update
sudo apt-get install nftables -y
```

## Step 2: View Current Ruleset
Check if any rules already exist.

- Run:
```bash
sudo nft list ruleset
```

- Is there an existing ruleset? (Yes/No)

<br>

## Step 3: Create a Table
Tables are used to organize firewall rules.

- Run:
```bash
sudo nft add table inet filter
```

- This creates a table named "filter" that works for IPv4 and IPv6.

- What table did you create? filter

<br>

## Step 4: Create a Chain
Chains control how packets are processed.

- Run:
```bash
sudo nft add chain inet filter input { type filter hook input priority 0 \; policy drop \; }
```

- This creates an input chain with a default policy of dropping traffic.

- What is the default policy? drop

<br>

## Step 5: Add Firewall Rules
Now we will allow specific types of traffic.

- Allow loopback traffic:
```bash
sudo nft add rule inet filter input iif lo accept
```

- Allow established connections:
```bash
sudo nft add rule inet filter input ct state established,related accept
```

- Allow ICMP (ping):
```bash
sudo nft add rule inet filter input ip protocol icmp accept
```

- How many rules did you add? 3

<br>

## Step 6: Review Ruleset
Verify that everything was added correctly.

- Run:
```bash
sudo nft list ruleset
```

- Look for:
  - inet filter table
  - input chain
  - your rules

- Do you see your rules listed? (Yes/No)

<br>

## Step 7: Test Connectivity
Now test if traffic is allowed.

- Run:
```bash
ping -c 4 8.8.8.8
```

- Did the ping work? (Yes/No)

<br>

## Step 8: Block Traffic (Optional Test)
To see how blocking works, remove the ICMP rule.

- Run:
```bash
sudo nft delete rule inet filter input handle <handle_number>
```

- Then test ping again:
```bash
ping -c 4 8.8.8.8
```

- Did the ping fail? (Yes/No)

<br>

## Step 9: Cleanup
Remove the table to reset the environment.

- Run:
```bash
sudo nft delete table inet filter
```

- Verify:
```bash
sudo nft list ruleset
```

- Is the ruleset empty? (Yes/No)

<br>

## Finished!

## Learning Objectives

- Understand how nftables replaces iptables
- Create and manage a ruleset
- Add and verify firewall rules
- Test allowed and blocked traffic

## Prerequisites

- Basic Linux terminal knowledge

## Lab Enviroment Setup

Kali Base
```bash
RUN sudo apt-get update -y
RUN sudo apt-get install nftables -y
RUN sudo apt-get install iputils-ping -y
RUN sudo apt-get install net-tools -y
```

## Assessment

### Assessment 1:
Run:
```bash
sudo nft list ruleset
```

### Assessment 2:
Create a table and input chain

### Assessment 3:
Add rules for loopback, established connections, and ICMP

### Assessment 4:
Verify rules using:
```bash
sudo nft list ruleset
```

### Assessment 5:
Test connectivity using ping

## FAQs

### Why is nftables considered modern?
It combines multiple firewall tools into one system and uses a simpler, more flexible structure.

### Why set the default policy to drop?
It blocks all traffic unless explicitly allowed, which improves security.

### What is a ruleset?
A ruleset is the complete set of tables, chains, and rules currently active in nftables.

## Related Skills & Roles

Cybersecurity Analyst  
Network Administrator  
Security Engineer  
System Administrator
