# SSL/TLS Basics

## Background
SSL (Secure Sockets Layer) and TLS (Transport Layer Security) are protocols used to secure communication between a client and a server. Today, TLS is the modern and secure version. It protects data by encrypting traffic, verifying server identity using certificates, and preventing attacks such as eavesdropping and data tampering. This module demonstrates how secure connections work and how TLS protects communication over the internet.

---
## Step 1: Establish a Secure Connection
Run the following command in Kali:

```bash
openssl s_client -connect google.com:443
```
- This command connects to a secure server using HTTPS and performs a TLS handshake.

### Reflection Questions:
- What server are you connecting to in this command?

## Step 2: View Certificate Information
- Look through the output of the command.

- You should see certificate details, including the certificate chain and server information.

### Reflection Questions:
- What information does the certificate provide about the server?

## Step 3: Identify the TLS Version
In the output, find the section that shows the TLS protocol version (for example, TLSv1.2 or TLSv1.3).

- This confirms that the connection is encrypted.

### Reflection Questions:
- What TLS version is shown in the output?

## Step 4: Understand the Purpose of TLS
TLS secures communication by encrypting data and verifying the server's identity using certificates.

This prevents attackers from reading or modifying data during transmission.

### Reflection Questions:
- Why is TLS important for secure communication?

