---
title: "Networking Tools"
id: "networking-tools"
Author: "Ayden Moore"
Date: "3/10/2026"
---
## Background Objectives
Wireshark is a tool used to observe network traffic. Filters can be applied to look for specific packets and information. This makes it easier to find if or when a specific connection was made on the network. Wireshark can be used for red team or blue team objectives in cyber security evaluations.

## Step 1: Open the Captured Packets
We must open the captured packets with wireshark.

- In a console window:
```bash
sudo wireshark -r http.pcap
```

## Step 2: Recognizing Wireshark

Wireshark has many features, lets become familiar with some of them.

- In the bottom right corner there is a section that says the number of packets.
    - *How many packets are there in this capture?* 43
<br>

- On the top of wireshark there are different options, select the statistic option and choose conversations. The conversations window will tell how many different streams of packets there are.
    - *How many conversations were in this capture?* 1
<br>

- In the options on the top of the screen select view and choose coloring rules. In wireshark the packets will be different color depending on the type of packet, this makes it easier to differentiate them. These can be changed by the user to fit their preference.
    - *What is the default color of the TEXT for a bad TCP?* Red

## Step 3: Applying Filters in Wireshark
Now that we have become familiar with the look of wireshark lets use some of the tools to help find specific packets.

- Above where the packets are displayed there is a text box where packet filters can be input. input the filter by typing "http" in the text box.
    - *how many http packets are there?* 4
<br>

- filters can be more specific by typing && after the filter. try it with the filter tcp&&frame.len==1434
    - *How many packets are displayed with these filters?* 13

## Step 4: Analyzing packets
Wireshark will give information about each packet allowing us to do analysis of a network situation. We will look at where we can find this information now.

- On the left side of the screen it will display the frame number of each packet in the order they came in. Click on the frame 3 packet. In the bottom right of the screen it will open a box and show the data that was transferred in hexadecimal. Each value coresponds to a part of the packet and will be highlighted when selected.
<br>

- On the bottom left of the screen a box has opened and that is the value from the hexadecimal translated into an easier to read format. There are drop down menus that get into more specific details as they are opened. Click the section labeled *Transmission Control Protocol* or the 4th drop down section.
    - *What are the first two bytes of this section highlighted in the hexadecimal box?(1 byte = 1 character 00 = 2 bytes)* 0d
<br>

- Looking within the *Transmission Control Protcol* dropdown.
    - *What is the hexidecimal value of the flags? (0x___)* 0x010
<br>

- Lets leave frame 3 and look at frame 4. select frame 4 in the colored section, now look under the *Transmission Control Protocol* dropdown for this frame.
    - *What is the value in the section labeled "Host:"* \www.ethereal.com\r\n
<br>

- Now that we have looked at the individual packets, lets look at them altogether. right click on frame 4 and press follow, then select http stream. This pulls up a window, it appears to be mostly html from a website. Look through this and see what you can gather about the website.
    - *What is contained within the first instance of h2 brackets?   (< h2> ______ </ h2>)* Ethereal

## Finished!


## Learning Objectives

- Become familiar with **WireShark** Functionality.
- Use **Wireshark** to identify different packets.
- Filter packets to find specific source of network traffic.
- investigate the different sections of a packet.

## Prerequisites

- **None**

## Lab Enviroment Setup

Kali Base
```bash
RUN sudo apt-get install wireshark -y
RUN sudo apt-get install iputils-ping -y

```
