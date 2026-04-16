--- 
title: "Firewall Management with iptables"
id: "firewall-management-iptables"
author: "Toby Knudsen"
date: "2026-04-07"
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

## Assessment
### Assessment 1:
- iptables -L -v
Identify default chains

### Assessment 2:
- Set INPUT policy to DROP
- Verify change

### Assessment 3:
- Add rule to allow localhost traffic

### Assessment 4:
- Add rule for established connections
- Confirm connectivity still works

### Assessment 5:
- Add and test ICMP rule

### Assessment 6:
- Add a rule to block a specific IP

### Assessment 7:
- Flush all rules and restore default policy

## FAQs
What is iptables?
- iptables is a Linux firewall tool used to control incoming and outgoing network traffic based on defined rules.

What are chains in iptables?
- Chains are sets of rules that determine how packets are processed, such as INPUT, OUTPUT, and FORWARD.

What does a default policy do?
- A default policy defines what happens to traffic that does not match any rules, such as ACCEPT or DROP.

Why use a default DROP policy?
- It blocks all traffic unless explicitly allowed, improving overall security.

What is ICMP used for?
- ICMP is used for network diagnostics, such as the ping command.

### Related Skills & Roles
- Cybersecurity Analyst
- Network Administrator
- Security Engineer
- System Administrator
