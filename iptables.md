
# Firewall Management with iptables


## Background

iptables is a legacy firewall tool used in Linux systems to control incoming and outgoing network traffic. It works by defining rules that either allow or block packets based on criteria such as IP address, protocol, port number, or connection state. These rules are organized into chains like INPUT, OUTPUT, and FORWARD, which determine how traffic is handled depending on whether it is entering, leaving, or passing through the system.

Even though newer tools like nftables have been developed to simplify firewall management, iptables is still widely used and important to understand. Many systems and environments continue to rely on it, and it provides a strong foundation for learning how firewalls operate. In this lab, you will create and modify basic firewall rules to better understand how traffic can be controlled and secured.


### Background Objectives

iptables is a legacy firewall tool used in Linux systems to control incoming and outgoing traffic. It works by defining rules that either allow or block packets based on things like IP address, protocol, or port. Even though newer tools like nftables exist, iptables is still widely used and important to understand.

## Step 1: View Current Rules
---
Check the current iptables rules to see what is already configured.
```bash
sudo iptables -L -v
```
Look at the default chains such as INPUT, OUTPUT, and FORWARD. These control how traffic is handled.

### Reflection Questions
- What are the three default chains shown in iptables?

- What does each chain control in terms of traffic flow?
## Step 2: Set Default Policy
---
Set the default policy for incoming traffic to DROP so that all traffic is blocked unless explicitly allowed.
```bash
sudo iptables -P INPUT DROP
```
Verify the change by running:
```bash
sudo iptables -L
```
### Reflection Questions
- What does setting the default policy to DROP do?

- Why is a default-deny approach considered more secure?
## Step 3: Allow Localhost Traffic
---
Allow traffic from the local machine so basic system processes continue to work.
```bash
sudo iptables -A INPUT -i lo -j ACCEPT
```
### Reflection Questions
- What is the loopback interface (lo)?

- Why would blocking localhost traffic cause issues?
## Step 4: Allow Established Connections
---
Allow responses to outgoing connections so normal browsing and communication works.
```bash
sudo iptables -A INPUT -m conntrack --ctstate ESTABLISHED,RELATED -j ACCEPT
```
Reflection Questions
- What are “ESTABLISHED” and “RELATED” connections?

- Why is this rule necessary for normal network usage?
## Step 5: Allow ICMP (Ping)
---
Allow ping requests to test connectivity.
```bash
sudo iptables -A INPUT -p icmp -j ACCEPT
```
Test this by pinging your machine from another system if available.

## Reflection Questions
- What protocol does ping use?

- What does a successful ping tell you about connectivity?
## Step 6: Block Specific Traffic
---
Block a specific IP address to simulate restricting access.
```bash
sudo iptables -A INPUT -s 192.168.1.100 -j DROP
```
Replace the IP if needed depending on your environment.

### Reflection Questions
- What does this rule do to traffic from that IP address?

- In what situations would blocking a specific IP be useful?
## Step 7: Verify Rules
---
List all rules again to confirm everything is applied correctly.
```bash
sudo iptables -L -v
```
Make sure your rules appear in the correct order.

### Reflection Questions
- Why does the order of rules matter in iptables?

- What could happen if rules are placed in the wrong order?
## Step 8: Flush Rules (Reset)
---
Clear all rules to return the system to its original state.
```bash
sudo iptables -F
sudo iptables -P INPUT ACCEPT
```
Verify that rules have been removed:
```bash
sudo iptables -L
```
### Reflection Questions
- What does flushing the rules do?

- Why is it important to reset configurations after testing?
