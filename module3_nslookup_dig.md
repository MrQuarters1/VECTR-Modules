---
title: "DNS Resolution with Nslookup and Dig"
id: "dns-resolution-with-nslookup-and-dig"
author: "Ahmad Hasan"
date: "2026-03-24"
version: "1.0"
---

## Learning Objectives
- Use `nslookup` and `dig` to verify DNS resolution.
- Identify whether a connectivity issue is actually a DNS problem.
- Compare DNS responses from different servers.

## Prerequisites
- Basic familiarity with a terminal
- Basic understanding of domain names, IP addresses, and DNS

## Lab Environment Setup
Kali Base
```bash
RUN sudo apt-get update
RUN sudo apt-get install dnsutils -y
```

Windows Base
- Windows 11 VM with Command Prompt or PowerShell available
- `nslookup` available by default

## Background
This lab supports the NEST Capstone project in the NebraskaCyber MATRIX VECTR environment. The project is focused on building hands-on networking modules in an isolated sandbox using Windows and Kali Linux virtual machines. The purpose of this lesson is to help learners diagnose DNS-related failures inside the sandbox.

These tools are important because they let students answer questions such as:
- Does the hostname resolve correctly?
- Which DNS server is answering the query?
- Does the service fail by name but work by IP address?
- Is the issue caused by DNS rather than routing or host availability?

## Assessment
### Assessment 1
- Run `nslookup`
- Identify whether a hostname resolves

### Assessment 2
- Run `dig`
- Identify which DNS server answered and what record was returned

### Assessment 3
- Use `nslookup` and `dig` together
- Diagnose whether the problem is caused by incorrect or missing DNS resolution

## Step 1: Query a Hostname with Nslookup
Use `nslookup` to test whether a hostname resolves correctly.

```bash
nslookup example.com
```

Review the following:
- Whether the hostname resolves
- Which IP address is returned
- Which DNS server answered the query

If the name does not resolve, the likely issue is DNS rather than basic network connectivity.

## Step 2: Query a Hostname with Dig
Use `dig` for more detailed DNS output.

```bash
dig example.com
```

Review the following:
- The answer section
- Returned IP address or records
- Query status
- DNS server used for the response

## Step 3: Query a Specific DNS Server
You can test a specific DNS server directly.

```bash
dig @8.8.8.8 example.com
```

Compare:
- Whether the hostname resolves
- Which IP address is returned
- Whether the answer changes between DNS servers

This helps identify whether the problem is with the local DNS server, the DNS record itself, or the client configuration.

## Step 4: Apply the Troubleshooting Process
Use the following order when diagnosing a name resolution problem in the sandbox:

1. Test the hostname with `nslookup`
2. Verify the result with `dig`
3. Compare responses from different DNS servers if needed
4. Determine whether the issue is incorrect DNS configuration, a bad record, or DNS server failure

This workflow helps learners distinguish DNS issues from routing or host availability problems.

## Challenge Task
A web application in the sandbox works by IP address but not by hostname.

Use the CLI tools in this lesson to answer the following:
- Does the hostname resolve?
- Which DNS server is responding?
- Is the returned IP address correct?
- Does the response change when using a different DNS server?

Document your commands, findings, and final diagnosis.

## FAQs

### Why use both `nslookup` and `dig`?
Both query DNS, but `dig` provides more detailed output that is useful for troubleshooting and validation.

### Why would a service work by IP but not by hostname?
That usually indicates a DNS issue rather than a routing or host availability problem.

### Why is DNS troubleshooting its own module?
DNS failures are very common in real networks, and name resolution problems can look like connectivity failures until they are tested directly.

## Related Skills & Roles
- Network Administrator
- Cybersecurity Analyst
- Cybersecurity Engineer
- SOC Analyst
- Penetration Tester
