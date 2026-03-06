# Load Balancer Setup Using Nginx Reverse Proxy

## Overview

This document explains how to configure Nginx as a reverse proxy for two backend applications.
```
sudo apt update && sudo apt upgrade -y
```
## Step 1 Install Nginx
```
sudo apt install nginx -y
sudo nano /etc/nginx/conf.d/loadbalancer.conf
```
## Step 2 Configure Nginx
```
upstream backend_servers {
    server 192.168.x.x;
    server 192.168.x.x;
}

server {
    listen 80;

    location / {
        proxy_pass http://backend_servers;

        proxy_set_header Host $host;
        proxy_set_header X-Real-IP $remote_addr;
        proxy_set_header X-Forwarded-For $proxy_add_x_forwarded_for;
    }
}

```
## Step 3 Test Configuration
```
sudo nginx -t
sudo systemctl restart nginx
sudo rm /etc/nginx/sites-enabled/default
```
## Step 4 remove default file
```
sudo rm /etc/nginx/sites-enabled/default
```
## Nginx Error check
```
sudo tail -f /var/log/nginx/error.log
```