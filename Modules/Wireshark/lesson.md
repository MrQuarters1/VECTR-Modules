## Step 2 Reflection Questions
- *How many packets are there in this capture?* 43

- *How many conversations were in this capture for ethernet?* 1

- *What is the default color of the TEXT for a bad TCP?* Red

## Step 3 Reflection Questions 

- *how many http packets are there?* 4

- *How many packets are displayed with these filters?* 13

## Step 4 Relection Questions

- *What is the first row in the *Transmission Control Protocol* dropdown labeled?* 
Source port:

<br> 

- *Looking within the *Transmission Control Protcol* dropdown of frame 3* *What is the value in the section labeled "Destination port:"* 
80

<br>

- *What is the first word when following the HTTP stream in this capture*
GET 


## Learning Objectives

- Become familiar with **WireShark** Functionality.
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
