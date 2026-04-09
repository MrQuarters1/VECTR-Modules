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