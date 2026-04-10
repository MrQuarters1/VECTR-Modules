# Modernization with nftables

### Background

nftables is the modern firewall framework used in Linux and is designed to replace older tools like iptables. Instead of relying on multiple separate utilities, nftables combines everything into a single system that uses tables, chains, and rules to manage traffic. This structure makes firewall configurations more organized, consistent, and easier to understand compared to older approaches.

Firewalls play an important role in controlling network traffic by allowing or blocking packets based on defined rules. nftables improves this process by providing more flexibility and efficiency when creating and managing these rules. In this lab, you will build a basic ruleset, allow specific types of traffic, and test how those rules impact connectivity.

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

- What could happen if you add new rules without knowing the current configuration?

## Step 2: Create a Table
Tables are used to organize firewall rules.
```bash
Run:  
sudo nft add table inet filter  
```
This creates a table named "filter" that works for IPv4 and IPv6.

What table did you create? filter

### Reflection Questions
- How does organizing rules into tables help with firewall management?

- Why might separating rules into different tables be useful in larger systems?

## Step 3: Create a Chain
Chains control how packets are processed.
```bash
Run:  
sudo nft add chain inet filter input { type filter hook input priority 0 \; policy drop \; }  
```
This creates an input chain with a default policy of dropping traffic.

What is the default policy? drop

### Reflection Questions
- Why is a default drop policy considered more secure?

- What would be the risk of using a default accept policy instead?

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

### Reflection Questions
- What types of traffic did you allow and why are they necessary?

- What would break if one of these rules was missing?

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

- How can reviewing the ruleset help identify configuration errors?

## Step 6: Test Connectivity
Now test if traffic is allowed.
```bash
Run:  
ping -c 4 8.8.8.8  
```
Did the ping work? (Yes/No)

### Reflection Question
- What does a successful ping tell you about your firewall rules?

- What might it indicate if the ping fails unexpectedly?

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

- How does this demonstrate the importance of individual firewall rules?

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

- What issues could occur if old firewall rules are left in place?


