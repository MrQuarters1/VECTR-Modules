author: "Toby Knudsen"
date: "2026-04-08"
version: "1.0"
---

## Learning Objectives
- Understand how iptables is used for firewall management in Linux
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
```
### Assessment 1:
```bash
Run iptables -L -v
```
Identify default chains
### Assessment 2:
```bash
Set INPUT policy to DROP
```
Verify change
### Assessment 3:
```bash
Add rule to allow localhost traffic
```
### Assessment 4:
```bash
Add rule for established connections
```
Confirm connectivity still works
### Assessment 5:
```bash
Add and test ICMP rule
```
### Assessment 6:
```bash
Add a rule to block a specific IP
```
### Assessment 7:
```bash
Flush all rules and restore default policy
```