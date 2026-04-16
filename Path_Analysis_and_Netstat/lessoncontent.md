# Cybersecurity Lab: Path Analysis and Connection Visibility

## Background
After basic connectivity checks, the next step is to understand **where** traffic stops and **what** is happening on the endpoint. This lab introduces **traceroute**, **tracert**, and **netstat**.

- **traceroute** is commonly used on Linux.
- **tracert** is commonly used on Windows.
- **netstat** is used to inspect active connections, listening ports, and local network activity.

These tools help answer questions such as:
- Where does the traffic stop?
- Is a router, hop, or segment blocking communication?
- Is the expected service actually listening?
- Are there unexpected open ports or active connections?

---
## Step 1: Trace the Path on Kali with traceroute
Open a terminal on the Kali VM and run:

```bash
traceroute <target_ip>
```

Review:
- The number of hops
- The last successful hop
- Timeouts or unreachable messages

### Reflection Questions:
- What was the last hop that responded?
- What might repeated timeouts indicate?
- How could segmentation affect the output?

---
## Step 2: Trace the Path on Windows with tracert
Open **Command Prompt** or **PowerShell** on the Windows VM and run:

```powershell
tracert <target_ip>
```

Compare the output to what you see in Linux.

### Reflection Questions:
- Does the path look similar to the Kali result?
- At what point does the traffic appear to stop?
- What might a failed path say about the gateway or router configuration?

---
## Step 3: Inspect Active Connections with netstat
Now inspect the host for active connections and listening services.

### On Kali
```bash
netstat -tunlp
```

### On Windows
```powershell
netstat -ano
```

Look for:
- Listening ports
- Established connections
- Local and foreign addresses
- Process identifiers on Windows

### Reflection Questions:
- Which ports are listening?
- Is the expected service running?
- Are there any connections you did not expect to see?

---
## Step 4: Use the Tools Together
Use the following order when diagnosing a path or service issue:

1. Run `traceroute` or `tracert`
2. Identify the last successful hop
3. Decide whether the issue looks like routing, blocked forwarding, or segmentation
4. Run `netstat`
5. Verify whether the expected service is listening on the target host

### Reflection Questions:
- Why is it helpful to use both path analysis and port visibility?
- Could the route be valid while the service is still unavailable?

---
## Challenge Task
A service in the sandbox is unreachable from another host.

Use the tools in this lesson to answer:
- Where does the route stop?
- Is there evidence of segmentation or blocked forwarding?
- Is the expected service listening on the destination host?
- Are there any unexpected open ports or active connections?

Document your commands, findings, and final diagnosis.
