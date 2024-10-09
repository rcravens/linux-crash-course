# Chapter 15: Nginx Installation and Management

<a href="README.md">&laquo; main menu</a>

## 15.1 Introduction to Nginx
- **Purpose**
  - Nginx is a high-performance web server and reverse proxy server known for its scalability and efficiency.
  - Commonly used for serving static content, load balancing, and as a reverse proxy.

## 15.2 Installing Nginx
- **On Debian/Ubuntu**
  - **Update Package Index**:
    ```bash
    sudo apt update
    ```
  - **Install Nginx**:
    ```bash
    sudo apt install nginx
    ```
  - **Start and Enable Nginx**:
    ```bash
    sudo systemctl start nginx
    sudo systemctl enable nginx
    ```
  - **Explanation**: Installs Nginx and ensures it starts on boot.

- **On CentOS/RHEL**
  - **Install EPEL Repository**:
    ```bash
    sudo yum install epel-release
    ```
  - **Install Nginx**:
    ```bash
    sudo yum install nginx
    ```
  - **Start and Enable Nginx**:
    ```bash
    sudo systemctl start nginx
    sudo systemctl enable nginx
    ```

## 15.3 Basic Nginx Configuration
- **Configuration File Location**
  - **Main Configuration File**:
    - `/etc/nginx/nginx.conf`
  - **Site-Specific Configuration**:
    - `/etc/nginx/sites-available/`
    - `/etc/nginx/sites-enabled/`
  
- **Default Server Block**
  - **Location**: `/etc/nginx/sites-available/default` (Debian/Ubuntu) or `/etc/nginx/nginx.conf` (CentOS/RHEL)
  - **Example Configuration**:
    ```nginx
    server {
        listen 80;
        server_name example.com;
        
        location / {
            root /var/www/html;
            index index.html index.htm;
        }
    }
    ```
  - **Explanation**:
    - **listen 80**: Listens on port 80 (HTTP).
    - **server_name**: Specifies the domain name for the server.
    - **location /**: Configures the root directory and default index files.

- **Testing Configuration**
  - **Syntax Check**:
    ```bash
    sudo nginx -t
    ```
  - **Reload Configuration**:
    ```bash
    sudo systemctl reload nginx
    ```
  - **Explanation**: `nginx -t` checks for syntax errors, and `systemctl reload` applies configuration changes without restarting.

## 15.4 Managing Nginx
- **Starting, Stopping, and Restarting**
  - **Start Nginx**:
    ```bash
    sudo systemctl start nginx
    ```
  - **Stop Nginx**:
    ```bash
    sudo systemctl stop nginx
    ```
  - **Restart Nginx**:
    ```bash
    sudo systemctl restart nginx
    ```
  - **Explanation**: Use `systemctl` to control the Nginx service.

- **Viewing Status and Logs**
  - **Check Status**:
    ```bash
    sudo systemctl status nginx
    ```
  - **Access Logs**:
    - **Access Log**: `/var/log/nginx/access.log`
    - **Error Log**: `/var/log/nginx/error.log`
  - **Explanation**: Logs provide information on requests and errors.

## 15.5 Advanced Configuration
- **Reverse Proxy Setup**
  - **Example Configuration**:
    ```nginx
    server {
        listen 80;
        server_name proxy.example.com;
        
        location / {
            proxy_pass http://backend-server;
            proxy_set_header Host $host;
            proxy_set_header X-Real-IP $remote_addr;
            proxy_set_header X-Forwarded-For $proxy_add_x_forwarded_for;
        }
    }
    ```
  - **Explanation**:
    - **proxy_pass**: Forwards requests to the backend server.
    - **proxy_set_header**: Passes original headers to the backend server.

- **Load Balancing**
  - **Example Configuration**:
    ```nginx
    upstream backend {
        server backend1.example.com;
        server backend2.example.com;
    }
    
    server {
        listen 80;
        server_name loadbalancer.example.com;
        
        location / {
            proxy_pass http://backend;
        }
    }
    ```
  - **Explanation**: Configures load balancing across multiple backend servers.

## 15.6 Securing Nginx
- **Enabling SSL/TLS**
  - **Generate Self-Signed Certificate**:
    ```bash
    sudo openssl req -new -x509 -days 365 -nodes -out /etc/nginx/ssl/nginx.crt -keyout /etc/nginx/ssl/nginx.key
    ```
  - **Example SSL Configuration**:
    ```nginx
    server {
        listen 443 ssl;
        server_name secure.example.com;
        
        ssl_certificate /etc/nginx/ssl/nginx.crt;
        ssl_certificate_key /etc/nginx/ssl/nginx.key;
        
        location / {
            root /var/www/html;
        }
    }
    ```
  - **Explanation**: Configures SSL/TLS for secure HTTP connections.

- **Implementing Security Headers**
  - **Example Configuration**:
    ```nginx
    server {
        listen 80;
        server_name secure.example.com;
        
        add_header X-Content-Type-Options "nosniff";
        add_header X-XSS-Protection "1; mode=block";
        add_header X-Frame-Options "DENY";
        
        location / {
            root /var/www/html;
        }
    }
    ```
  - **Explanation**: Adds security headers to protect against certain web vulnerabilities.

## 15.7 Conclusion
Nginx is a versatile web server and reverse proxy with numerous features for optimizing and securing web traffic. By mastering installation, basic configuration, advanced features, and security practices, you can effectively manage and deploy Nginx in various scenarios.

- **Key Takeaways**:
  - **Installation**: Understand installation steps for different distributions.
  - **Configuration**: Set up basic and advanced server blocks.
  - **Management**: Use `systemctl` for service management and review logs.
  - **Security**: Implement SSL/TLS and security headers.

Regularly update your Nginx configuration and practices to keep up with evolving security standards and performance optimizations.

<a href="README.md">&laquo; main menu</a>