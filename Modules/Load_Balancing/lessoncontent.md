# Cybersecurity Lab: Understanding Reverse Proxies with NGINX

## Background
A reverse proxy is a useful network tool that enhances security and performance of a web server. Reverse proxies do so by acting as load balancers, SSL terminators, web caches, and anonymizers. Reverse proxies act as a layer in front of your web server rerouting traffic to the correct location.

This lab will outline the basic steps to setup a reverse proxy on a local network with NGINX to act as a load balancer.

---
## Step 1: Edit the Local Hosts File
Ideally you would use a purchased domain for your web server. In place of that we will edit a local file to resolve our ip to our chosen domain name.
- Edit the /etc/hosts file by adding an entry to the end of the file. ```127.0.0.1     example.com```
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

### Step 2: Start Sample Python Servers
To test our reverse proxy later with load balancing we will use a two similar python http servers with slightly different outputs.
- In a console window:
```bash
cd ~/Content/server1 && python -m http.server 8000 --bind 127.0.0.1
```
- In a new console window:
```bash
cd ~/Content/server2 && python -m http.server 8001 --bind 127.0.0.1
```
This will create a server available at http://localhost:8000 and http://localhost:8001.
- Run the following command to ensure that the first server is running properly.
```bash
curl localhost:8000
```
- Then run this command for the other server
```bash
curl localhost:8001
```

### Reflection Questions:
- Why would a user want to run multiple instances of the same server preferably on different machines?

---
## Step 3: Create a Configuration for NGINX Reverse Proxy
A configuration file is required to create the Reverse Proxy. We are not using NGINX to serve the html. This simplifies our configuration.
- In a new console window:
```bash
cd /etc/nginx/sites-available
```
- Next create a file for our configuration.
```bash
sudo touch hello_world.conf && sudo nano hello_world.conf
```
```nginx
upstream my_python_webservers {
    server localhost:8000;
    server localhost:8001;
}
server {
    listen 80;
    server_name example.com www.example.com;

    location / {
        proxy_pass http://my_python_webservers;
        proxy_set_header Host $host;
        proxy_set_header X-Real-IP $remote_addr;
        proxy_set_header X-Forwarded-For $proxy_add_x_forwarded_for;
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
- If nginx was already running and causes errors we can reload with a different command.
```bash
sudo nginx -s reload
```
- We can test to see if the changes are working by running curl on example.com.
```bash
curl example.com
```

### Reflection Questions:
- How might we add a third server running on a seperate machine to the configuration file?
- In a production environment how would you modify the configuration file to resolve to instances of the server on seperate machines?