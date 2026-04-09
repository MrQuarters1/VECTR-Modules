---
title: "Networking Tools"
id: "networking-tools"
author: "Ayden Moore"
date: "2026-04-07"
version: "1.0"
---
## Learning Objectives

- Become familiar with **WireShark** functionality.
- Use **Wireshark** to identify different packets.
- Filter packets to find specific source of network traffic.
- investigate the different sections of a packet.

## Prerequisites

- Needs a folder called content with the http.cap file

## Lab Enviroment Setup

Kali Base
```bash
RUN sudo apt-get install wireshark -y
RUN sudo apt-get install iputils-ping -y

```
## Assessment

### Assessment 1:
 - run command to open wireshark.

### Assessment 2:
 - Use Wireshark tools to gather info on group of packets.
#### Reflection Questions Answers
- *How many packets are there in this capture?* **43**

- *How many conversations were in this capture for ethernet?* **1**

- *What is the default color of the TEXT for a bad TCP?* **Red**

### Assessment 3: 
- Use filters to reduce clutter.

#### Reflection Questions Answers

- *how many http packets are there?* **4**

- *How many packets are displayed with these filters?* **13**

### Assessment 4:
 - Analyze individual packets.
#### Relection Questions Answers

- *What is the first row in the *Transmission Control Protocol* dropdown labeled?* 
**Source port:**


- *Looking within the *Transmission Control Protcol* dropdown of frame 3* *What is the value in the section labeled "Destination port:"* 
**80**


- *What is the first word when following the HTTP stream in this capture*
**GET** 

