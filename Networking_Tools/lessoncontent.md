# Cybersecurity Lab: Understanding Network Traffic and Basic Analysis

## Background
Information traveling across the network is sent in **packets**. By the nature of the Transfer Control Protocol (TCP) and the Internet Protocol (IP), the headers of these packets can be viewed by anyone who can intercept the packets. The content of a packet may be encrypted but that will not hide data like the source and destination of the packet as well as other data about the packet.

Networks form the backbone of modern communication. Monitoring and analyzing network traffic is a critical skill for cybersecurity professionals. This lab introduces students to packet capture (PCAP) and network analysis to identify normal activities. We will also examine network commands to route traffic.

---
## Step 1: Capturing Network Traffic
Snort is a multipurpose tool for capturing and analyzing network traffic. We are going to use it to collect traffic and save it to a file.
- In a console window:
```bash
sudo snort -i eth0 -L pcap
```
- Perform the following tasks while Snort is running:
    - Open a web browser and visit example.com
    - Conduct a quick Google search.
    - Send a simple ping command in the terminal:
```bash
ping -c 4 localhost
```
- Stop the packet capture by typing **ctrl + C** in the Snort terminal window.
- Note the name of the .pcap file
- We will also need to change the permissions of this file so we can view the contents.
```bash
ls
sudo chmod 755 log.pcap.XXXXXXXXXXXXX
```
- Use ***tab*** to autocomplete the log file name. Once you type **log** you can hit tab and it will fill in.

- Open Wireshark to view the packet contents.
```bash
wireshark log.pcap.XXXXXXXXXXXX
```


### Reflection Questions:
- What is the protocol for ping traffic?
- Can you spot your IP address in the list of packets?

## Step 2: Analyzing Captured Traffic
Now that we have a pcap file to analyze, we will use some of the built-in features of Wireshark to identify packets that might be interesting.

- Use the Filter Bar to apply these filters:
    - HTTP traffic: http
    - Ping requests (ICMP): icmp
    - Traffic from your IP: Replace <your_ip> in the filter: ip.src == <your_ip>
        - You can find your IP address by typing ifconfig in your terminal.

### Reflection Questions:
- How many ping packets did you send?
- Was there any web traffic?
- Do you notice any other protocols?

## Step 3: Exploring Network Routes and Domain Resolution
Routing and DNS are two critical components of computer networking. Routing determines how packets travel from source to destination. DNS (Domain Name System) resolves domain names into IP addresses. In this part of the lab, you will use several tools to examine routing paths, domain lookups, and the routes used by your system to access the internet.

- The traceroute tool shows the path your packets take to reach a domain, hop-by-hop.
- Open your terminal.

```bash
traceroute example.com
```

Unfortunately in our platform, traceroute will not give you full feedback. On a standard system you will see all of the **hops** between your computer and the server.

Knowing the IP address of your destination is necessary. The IP address is different than the URL (i.e. `www.google.com` is not the IP address). We use a service called DNS or the Domain Name System to resolve the common URL to the specific IP address.

You can directly query the DNS with the following command:
```bash
nslookup unomaha.edu
```

Similarly you can use a known DNS like Google's DNS [8.8.8.8](8.8.8.8) to lookup an IP address.

### Reflection Questions:
- What is the purpose of DNS
- How could DNS be misused to direct people to the wrong page?
- How difficult is DNS poisoning?

## Step 4: Domain Resolution with DIG
The dig command shows how DNS resolves a domain to an IP address.

In the terminal, run:
```bash
dig example.com
```
This will trace the full DNS resolution path from the root DNS servers.
```bash
dig google.com +trace
```

### Reflection Questions:
- What IP address was resolved for the domain?
- What is the TTL (Time to Live) for the record?
- What nameservers are involved in the trace?

## Step 5: Exploring Network Routes
Use ip route and netstat to view how your system routes traffic.
View the routing table:
```bash
ip route
```
View active connections and routing information:

```bash
netstat -rn
```
Identify the default gateway and interface used.

### Reflection Questions:
- What is your system’s default gateway?
- Which interface is used to reach external IPs?
- What local IP addresses are active?

