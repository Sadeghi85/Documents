# Installing Nginx on Ubuntu 22.04

### Step 1 – Installing Nginx
````
sudo apt update
sudo apt install nginx
````

### Step 2 – Adjusting the Firewall

```
sudo ufw app list
```

You should get a listing of the application profiles:
```
Output
Available applications:
  Nginx Full
  Nginx HTTP
  Nginx HTTPS
  OpenSSH
```
As demonstrated by the output, there are three profiles available for Nginx:

-   **Nginx Full**: This profile opens both port 80 (normal, unencrypted web traffic) and port 443 (TLS/SSL encrypted traffic)
-   **Nginx HTTP**: This profile opens only port 80 (normal, unencrypted web traffic)
-   **Nginx HTTPS**: This profile opens only port 443 (TLS/SSL encrypted traffic)

```
sudo ufw allow 'Nginx HTTP'
```

```
sudo ufw status
```

```
Output
Status: active

To                         Action      From
--                         ------      ----
OpenSSH                    ALLOW       Anywhere                  
Nginx HTTP                 ALLOW       Anywhere                  
OpenSSH (v6)               ALLOW       Anywhere (v6)             
Nginx HTTP (v6)            ALLOW       Anywhere (v6)
```

### Step 3 – Checking NGINX
```
systemctl status nginx
```

### Step 4 – Managing the Nginx Process
```
sudo systemctl stop nginx
sudo systemctl start nginx
sudo systemctl restart nginx
sudo systemctl reload nginx
sudo systemctl disable nginx
sudo systemctl enable nginx
```
