# Cybersecurity Lab: IP Configuration and Basic Reachability

## Background
When diagnosing a network issue, the first step is usually to confirm that the local machine is configured correctly and can reach other systems. This lab introduces three foundational networking tools: **ipconfig**, **ifconfig**, and **ping**.

- **ipconfig** is used on Windows to inspect IP settings.
- **ifconfig** is used on Linux to inspect interface settings.
- **ping** is used to test whether another host is reachable.

These tools help answer important troubleshooting questions:
- Does this host have a valid IP address?
- Is the subnet mask correct?
- Is a default gateway configured?
- Can the host reach another system?

---
## Step 1: Inspect Windows Network Configuration with ipconfig
Open **Command Prompt** or **PowerShell** on the Windows VM and run:

```powershell
ipconfig /all
```

Review the following values:
- IPv4 address
- Subnet mask
- Default gateway
- DNS servers
- Adapter name

### Reflection Questions:
- What is the IP address of the Windows host?
- What is the default gateway?
- How would a missing gateway affect connectivity?

---
## Step 2: Inspect Linux Network Configuration with ifconfig
Open a terminal on the Kali VM and run:

```bash
ifconfig
```

Identify the active interface and review:
- IPv4 address
- Netmask
- Broadcast address
- Interface status

### Reflection Questions:
- Which interface appears to be active?
- What is the IPv4 address on that interface?
- What happens if the interface is down or configured with the wrong network?

---
## Step 3: Test Local Reachability with ping
Use `ping` to confirm that the local network stack is working.

### On Kali
```bash
ping -c 4 127.0.0.1
```

### On Windows
```powershell
ping 127.0.0.1
```

A successful result confirms that the local TCP/IP stack is functioning.

### Reflection Questions:
- Why is `127.0.0.1` useful during troubleshooting?
- What does it mean if localhost does not respond?

---
## Step 4: Test Connectivity to Another Host
Now test connectivity to another host in the lab.

### Kali
```bash
ping -c 4 <target_ip>
```

### Windows
```powershell
ping <target_ip>
```

Use the results to identify:
- Whether the host responds
- Approximate latency
- Packet loss
- Whether the issue appears local or remote

### Reflection Questions:
- Did the target respond?
- Was there packet loss?
- Could a failed ping be caused by firewall rules rather than the host being down?

---
## Step 5: Use the Tools Together
Use the following order when troubleshooting a basic network problem:

1. Run `ipconfig /all` or `ifconfig`
2. Verify the IP address, subnet mask, and gateway
3. Run `ping 127.0.0.1`
4. Run `ping <target_ip>`
5. Decide whether the problem is caused by bad local configuration or simple connectivity loss

### Reflection Questions:
- Which command would you run first in a real troubleshooting scenario?
- Why is it helpful to confirm local settings before testing a remote system?

---
## Challenge Task
A host in the sandbox cannot reach an internal server.

Use the tools in this lesson to answer:
- Does the host have a valid local IP configuration?
- Is the subnet correct for the lab network?
- Is the default gateway present?
- Can the host reach the target by IP?

Document your commands, findings, and final diagnosis.
