# Basic Network Segmentation with Subnets

## Background Objectives
Network segmentation is used to divide a large network into smaller parts called subnets. This helps improve security and organization. By controlling communication between systems, segmentation prevents attackers from moving freely across the network. Subnets also reduce unnecessary traffic and improve network efficiency. For the purposes of this lab, the Windows machine will be treated as its own subnet.

---
## Step 1: Identify Network Information
Run the following command in Kali:

```bash
ip addr
```

- This command shows your network interface and IP address.

Run the following command in Windows

```bash
ipconfig
```

## Reflection Questions:
- What is the IP address of your Kali machine?
- What is the IP address of your Windows machine?

## Step 2: Test Connectivity
Run the following command in Kali:

```bash
ping <WINDOWS_IP_ADDR>
```
* This checks if Kali can communicate with the Windows machine.

## Reflection Questions:
- Was the ping successful?

## Step 3: Verify Communication
Run the following command in Windows Command Prompt:

```bash
ping <KALI_IP_ADDR>
```
- This tests communication from Windows to Kali.

## Reflection Questions:
- Can both systems communicate with each other?

## Step 4: Apply Network Control
On your Windows Machine.

1- Open **Windows Defender Firewall with Advanced Security**.

2- Go to **Inbound Rules**, then disable the following rule:

3- **File and Printer Sharing (Echo Request – ICMPv4-In)**

This blocks ping requests.

## Reflection Questions:
- What happens when ICMP traffic is blocked?

## Step 5: Test Segmentation
Run the following command again in Kali:

```bash
ping <WINDOWS_IP_ADDR>
```
This tests connectivity after applying firewall restrictions.
After blocking the firewall rule, ping should fail and show **100% packet loss**.
This demonstrates how communication between systems can be restricted.

## Reflection Questions:
- What happens after blocking ICMP traffic?
- How does blocking traffic **improve** network security?

