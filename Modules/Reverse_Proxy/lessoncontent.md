# Cybersecurity Lab: Understanding Reverse Proxies with NGINX

## Background
A reverse proxy is a useful network tool that enhances security and performance of a web server. Reverse proxies do so by acting as load balancers, SSL terminators, web caches, and anonymizers. Reverse proxies act as a layer in front of your web server rerouting traffic to the correct location.

This lab will outline the basic steps to setup a reverse proxy on a local network with NGINX.

---
## Step 1: Edit the Local Hosts File
Ideally you would use a purchased domain for your web server. In place of that we will edit a local file to resolve our ip to our chosen domain name.
- Edit the /etc/hosts file by adding an entry to the end of the file.
    - ```127.0.0.1     example.com```
```bash
sudo nano /etc/hosts
```
- If done correctly you should now be able to ping example.com and see ```<your_ip>``` in the results.
```bash
ping -c 4 example.com
```

### Reflection Questions:
- What is the purpose of adding an entry to the Local Hosts file?
- Why would ```dig example.com``` not resolve to ```<your_ip>```?

---
## Step 2: Start a Sample Server
To test our reverse proxy later we will use a simple "Hello World!" python http server.
- In a console window:
```bash
cd Content && python -m http.server 8000 --bind 127.0.0.1
```
This will create a server available at http://localhost:8000.
- Run the following command to ensure that it is running properly.
```bash
curl localhost:8000
```

### Reflection Questions:
- Why would a user want to avoid port forwarding port 8000?
- Would this setup be sufficient for a production environment?


---
## Step 3: Create a Configuration for NGINX Reverse Proxy
A configuration file is required to create the Reverse Proxy. We are not using NGINX to serve the html. This simplifies our configuration.
- In a console window:
```bash
cd /etc/nginx/sites-available
```
- Next create a file for our configuration.
```bash
sudo touch hello_world.conf && sudo nano hello_world.conf
```
```nginx
server {
    listen 80;
    server_name example.com www.example.com;

    location / {
        proxy_pass http://localhost:8000;
        proxy_set_header Host $host;
        proxy_set_header X-Real-IP $remote_addr;
        proxy_set_header X-Forwarded-For $proxy_add_x_forwarded_for;
        proxy_set_header X-Forwarded-Proto $scheme;
    }
}
```
- Next we must create a symbolic link to this file to the sites-enabled folder.
```bash
sudo ln -s /etc/nginx/sites-available/hello_world.conf /etc/nginx/sites-enabled/hello_world.conf
```
- Next we can test the configuration. If this returns any errors ensure that there are no typos in the file above.
```bash
sudo nginx -t
```
- Finally we can run nginx.
```bash
sudo nginx
```
- We can test to see if the changes are working by running curl on example.com. Run this a few times to see if both server1 and server2 are being accessed.
```bash
curl example.com
```

### Reflection Questions:
- Why might portforwarding all of your services be a bad idea?
- How might we modify the line with the proxy pass to resolve to a service running at http://192.168.0.2:3000