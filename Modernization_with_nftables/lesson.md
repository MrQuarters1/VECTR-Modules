---
title: "Modernization with nftables"
id: "modernization-with-nftables"
author: "Toby Knudsen"
date: "2026-04-08"
version: "1.0"
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
RUN sudo apt-get update -y
RUN sudo apt-get install nftables -y
RUN sudo apt-get install net-tools -y
```
## Assessments
### Assessment 1:
```bash
View current ruleset using nft list ruleset
```
### Assessment 2:
```bash
Create a table and input chain with a default drop policy
```
### Assessment 3:
```bash
Add rules for loopback, established connections, and ICMP traffic
```
### Assessment 4:
```bash
Verify rules using nft list ruleset
```
### Assessment 5:
```bash
Test connectivity using ping
```
### Assessment 6:
```bash
Remove a rule and observe the effect on connectivity
```
### Assessment 7:
```bash
Delete the table and confirm the ruleset is cleared
```
### FAQs

What is nftables?
nftables is the modern Linux firewall framework that replaces iptables and provides a unified way to manage filtering rules.

Why is nftables considered an improvement over iptables?
It simplifies rule management by combining multiple tools into one system and uses a more consistent structure.

What is a table in nftables?
A table is a container that holds chains and rules used to filter network traffic.

What is a chain?
A chain defines how packets are processed and includes a default policy such as accept or drop.

Why use a default drop policy?
It blocks all traffic unless explicitly allowed, which increases security.

### Related Skills & Roles
Cybersecurity Analyst
Network Administrator
Security Engineer
System Administrator
