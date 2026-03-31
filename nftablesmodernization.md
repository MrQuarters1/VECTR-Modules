---
title: "Modernization with nftables"
id: "modernization-with-nftables"
Author: "Toby Knudsen"
Date: "3/30/2026"
---

## Background Objectives
nftables is the newer version of firewall management in Linux and is meant to replace iptables. It allows you to create and manage firewall rules in a more organized way. In this lab, we will go through basic commands to view rules, create a simple ruleset, and understand how traffic is allowed or blocked.

## Step 1: Install nftables
First we need to make sure nftables is installed.

- In a terminal:
sudo apt-get update
sudo apt-get install nftables -y

- Check that it installed correctly:
nft --version

## Step 2: View Current Rules
Before making changes, we want to see what rules already exist.

- Run:
sudo nft list ruleset

- Is there an existing ruleset? (Yes/No)

<br>

## Step 3: Create a Table
nftables uses tables to organize rules.

- Run:
sudo nft add table inet filter

- This creates a table called filter.

- What table did you just create? filter

<br>

## Step 4: Create a Chain
Chains define how traffic is handled.

- Run:
sudo nft add chain inet filter input { type filter hook input priority 0; policy drop; }

- This creates an input chain that drops traffic by default.

- What is the default policy set to? drop

<br>

## Step 5: Add Basic Rules
Now we will allow certain types of traffic.

- Allow loopback traffic:
sudo nft add rule inet filter input iif lo accept

- Allow established connections:
sudo nft add rule inet filter input ct state established,related accept

- Allow ping traffic:
sudo nft add rule inet filter input ip protocol icmp accept

- How many rules have you added so far? 3

<br>

## Step 6: Review Rules
Now check your configuration.

- Run:
sudo nft list ruleset

- Look for:
  - inet filter table
  - input chain
  - your 3 rules

- Do you see your rules listed? (Yes/No)

<br>

## Step 7: Test Traffic
We will test if traffic is being allowed.

- Run:
ping 8.8.8.8

- Did the ping work? (Yes/No)

<br>

## Finished!

## Learning Objectives

- Understand what nftables is used for
- View and interpret a ruleset
- Create a table and chain
- Add basic firewall rules
- Test allowed traffic

## Prerequisites

- Basic Linux terminal knowledge

## Lab Enviroment Setup

Kali Base

RUN sudo apt-get update
RUN sudo apt-get install nftables -y
RUN sudo apt-get install iputils-ping -y

## Assessment

Assessment 1:
Run:
sudo nft list ruleset

Assessment 2:
Create a table and input chain

Assessment 3:
Add 3 rules (loopback, established, icmp)

Assessment 4:
Verify rules using:
sudo nft list ruleset

Assessment 5:
Run ping and confirm it works

## FAQs

### Why use nftables instead of iptables?
It is newer, more organized, and easier to manage larger rule sets.

### Why is the default policy set to drop?
It blocks everything unless explicitly allowed, which is more secure.

## Related Skills & Roles

Cybersecurity Analyst  
Network Administrator  
Security Engineer  
System Administrator  .

