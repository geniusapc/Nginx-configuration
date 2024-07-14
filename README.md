# Nginx-configuration

Verify that your Nginx build includes the stream module:

```
nginx -V 2>&1 | grep -- --with-stream

```

2. Edit the Nginx Configuration:

   Open your Nginx configuration file in a text editor with root or sudo privileges. For example:

   ``` sh
    sudo nano /etc/nginx/nginx.conf
   ```

3. Add the Stream Block:

   Add the stream block configuration to the file. Ensure it is placed outside of any http block, as it is for TCP/UDP and not HTTP.

   ``` nginx

    user nginx;
    worker_processes auto;
    error_log /var/log/nginx/error.log;
    pid /run/nginx.pid;

    events {
        worker_connections 1024;
    }

    stream {
        upstream tcp_server {
            server 192.168.1.100:3000;  # Replace with the IP address and port of your N      ode.js TCP server
    }

    server {
        listen 4000;  # Port number that Nginx listens on for incoming TCP connections

        proxy_pass tcp_server;
        proxy_connect_timeout 1s;
    }
    }

   ```




Remove  Nignx
```
   sudo apt remove nginx nginx-common nginx-full
```
Add the official Nginx repository:

```
sudo apt update
sudo apt install curl gnupg2 ca-certificates lsb-release
echo "deb http://nginx.org/packages/ubuntu $(lsb_release -cs) nginx" | sudo tee /etc/apt/sources.list.d/nginx.list
curl -fsSL https://nginx.org/keys/nginx_signing.key | sudo apt-key add -
sudo apt update
```
