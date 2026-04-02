---
title: "Modernization with nftables"
id: "modernization-with-nftables"
author: "Toby Knudsen"
date: "2026-03-30"
version: "1.3"
---

## Learning Objectives
- Understand how nftables modernizes Linux firewall management
- View and interpret an nftables ruleset
- Create tables, chains, and rules
- Test and verify allowed and blocked traffic

## Prerequisites
- none
## Lab Environment Setup

Kali Base
```bash
RUN sudo apt-get update
```
```bash 
RUN sudo apt-get install nftables -y
```
```bash
RUN sudo apt-get install net-tools -y
```
## Background Objectives
nftables is the modern replacement for iptables in Linux systems. Instead of using multiple tools and formats, nftables combines everything into a single framework that uses tables, chains, and rules. This makes firewall management more consistent and easier to understand. In this lab, you will build a basic ruleset from scratch and test how traffic is handled.


## Step 1: View Current Ruleset
Check if any rules already exist.
```bast
Run:  
sudo nft list ruleset  
```
Is there an existing ruleset? (Yes/No)

### Reflection Question
- Why is it important to check for an existing ruleset before making changes?

## Step 2: Create a Table
Tables are used to organize firewall rules.
```bash
Run:  
sudo nft add table inet filter  
```
This creates a table named "filter" that works for IPv4 and IPv6.

What table did you create? filter

### Reflection Question
- How does organizing rules into tables help with firewall management?

## Step 3: Create a Chain
Chains control how packets are processed.
```bash
Run:  
sudo nft add chain inet filter input { type filter hook input priority 0 \; policy drop \; }  
```
This creates an input chain with a default policy of dropping traffic.

What is the default policy? drop

### Reflection Question
- Why is a default drop policy considered more secure?

## Step 4: Add Firewall Rules
Now we will allow specific types of traffic.

Allow loopback traffic:
```bash
sudo nft add rule inet filter input iif lo accept  
```
Allow established connections:
```bash
sudo nft add rule inet filter input ct state established,related accept  
```
Allow ICMP (ping):
```bash
sudo nft add rule inet filter input ip protocol icmp accept  
```
How many rules did you add? 3

### Reflection Question
- What types of traffic did you allow and why are they necessary?

## Step 5: Review Ruleset
Verify that everything was added correctly.
```bash
Run:  
sudo nft list ruleset  
```
Look for:  
inet filter table  
input chain  
your rules  

Do you see your rules listed? (Yes/No)

### Reflection Question
- Why is verifying your ruleset important after making changes?

## Step 6: Test Connectivity
Now test if traffic is allowed.
```bash
Run:  
ping -c 4 8.8.8.8  
```
Did the ping work? (Yes/No)

### Reflection Question
- What does a successful ping tell you about your firewall rules?

## Step 7: Block Traffic (Optional Test)
To see how blocking works, remove the ICMP rule.
```bash
Run:  
sudo nft delete rule inet filter input handle <handle_number>  
```
Then test ping again:
```bash
ping -c 4 8.8.8.8  
```
Did the ping fail? (Yes/No)

### Reflection Question
- Why did removing one rule stop the ping from working?

## Step 8: Cleanup
Remove the table to reset the environment.
```bash
Run:  
sudo nft delete table inet filter  
```
Verify:
```bash
sudo nft list ruleset  
```
Is the ruleset empty? (Yes/No)

### Reflection Question
- Why is cleanup important after completing a lab?

## Finished!

## Assessment
Assessment 1:  
Run:  
sudo nft list ruleset  

Assessment 2:  
Create a table and input chain  

Assessment 3:  
Add rules for loopback, established connections, and ICMP  

Assessment 4:  
Verify rules using:  
sudo nft list ruleset  

Assessment 5:  
Test connectivity using ping  

## FAQs
Why is nftables considered modern?  
It combines multiple firewall tools into one system and uses a simpler, more flexible structure.  

Why set the default policy to drop?  
It blocks all traffic unless explicitly allowed, which improves security.  

What is a ruleset?  
A ruleset is the complete set of tables, chains, and rules currently active in nftables.  

## Related Skills & Roles
- Cybersecurity Analyst  
- Network Administrator  
- Security Engineer  
- System Administrator  
