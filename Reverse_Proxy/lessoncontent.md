# Cybersecurity Lab: Understanding Reverse Proxies with NGINX and Traefik

## Background
A reverse proxy is a useful network tool that enhances security and performance of a web server. Reverse proxies do so by acting as load balancers, SSL terminators, web caches, and anonymizers. Reverse proxies act as a layer in front of your web server rerouting traffic to the correct location.

This lab will outline the basic steps to setup a reverse proxy on a local network first with NGINX and then Traefik

---
## Step 1: Edit the Local Hosts File
Ideally you would use a purchased domain for your web server. In place of that we will edit a local file to resolve our ip to our chosen domain name.
- In a console window:
```bash
ifconfig
```
- Write down the public ip shown after inet. It should match 172.XXX.XXX.XXX.
- Next edit the /etc/hosts file by adding an entry to the end of the file.
    - ```<your_ip>     example.com```
```bash
sudo nano /etc/hosts
```
- If done correctly you should now be able to ping example.com
```bash
ping -c 4 example.com
```

### Reflection Questions:
- What is the purpose of adding an entry to the Local Hosts file?
- Why would ```dig example.com``` not resolve to ```<your_ip>```?