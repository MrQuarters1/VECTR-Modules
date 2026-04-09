---
title: "Load Balancing"
id: "load-balancing"
author: "Connor Licht"
date: "2026-04-09"
version: "1.0"
---

## Learning Objectives
- Use **Nginx** as a reverse proxy for load balancing.
- Edit the hosts file to resolve localhost to example.com.
- Add two web servers to the reverse proxy to test load balancing.

## Prerequisites
- A Folder called Content with two folders each containing an index.html should be added to home directory.

## Lab Environment Setup
Kali Base
```bash
RUN sudo apt-get install nginx -y
RUN sudo apt-get install iputils-ping -y
```

## Assessment
### Assessment 1:
- Edit the /etc/hosts file
- Add entry for localhost and example.com

### Assessment 2
- Start two simple python http servers

### Assessment 3
- Create an nginx configuration file in sites-available folder
- Create symbolic link in sites-enabled folder
- Run nginx command
- Test with curl command a few times to verify load balancing

## FAQs

## Related Skills & Roles
- System Administrator
- Developer Operations

