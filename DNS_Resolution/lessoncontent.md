# Cybersecurity Lab: DNS Resolution with Nslookup and Dig

## Background
DNS, or the **Domain Name System**, translates human-readable names into IP addresses. A system may have full IP connectivity and still fail to reach a service if DNS is misconfigured. This lab introduces **nslookup** and **dig** as core tools for diagnosing name resolution problems.

These tools help answer questions such as:
- Does the hostname resolve?
- Which DNS server answered the query?
- Is the returned IP address correct?
- Is the problem caused by DNS rather than routing or host availability?

---
## Step 1: Query a Hostname with nslookup
Open a terminal and run:

```bash
nslookup example.com
```

Review:
- The responding DNS server
- The resolved IP address
- Whether the lookup succeeds or fails

### Reflection Questions:
- Which DNS server responded?
- What IP address was returned?
- What would a failed lookup suggest?

---
## Step 2: Query a Hostname with dig
On Kali, use `dig` for more detailed output.

```bash
dig example.com
```

Review:
- The answer section
- Query status
- Returned records
- The responding server

### Reflection Questions:
- What status did `dig` return?
- What records appeared in the answer section?
- How is this output different from `nslookup`?

---
## Step 3: Query a Specific DNS Server
You can direct a query to a specific DNS server.

```bash
dig @8.8.8.8 example.com
```

Compare the results with the default resolver.

### Reflection Questions:
- Did the answer change when querying another DNS server?
- What could different answers tell you about the environment?

---
## Step 4: Use the Tools Together
Use the following order when diagnosing a DNS problem:

1. Run `nslookup`
2. Confirm the result with `dig`
3. Query a specific DNS server if needed
4. Decide whether the issue is caused by bad records, resolver failure, or client DNS configuration

### Reflection Questions:
- Why is it helpful to compare DNS responses from different servers?
- How can DNS issues look like general connectivity failures?

---
## Challenge Task
A web application in the sandbox works by IP address but not by hostname.

Use the tools in this lesson to answer:
- Does the hostname resolve?
- Which DNS server responds?
- Is the returned IP address correct?
- Does the answer change when using a different DNS server?

Document your commands, findings, and final diagnosis.
