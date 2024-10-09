# Chapter 20: Final Projects

<a href="README.md">&laquo; main menu</a>

## 20.1 Introduction to Final Projects
- **Purpose**
  - The final projects are designed to consolidate your knowledge and skills acquired throughout the course.
  - They provide practical experience by applying various Linux and software management techniques to real-world scenarios.

## 20.2 Project 1: LAMP Stack Deployment
- **Objective**
  - Set up a complete LAMP (Linux, Apache, MySQL, PHP) stack on a Linux server.
- **Requirements**
  - Install and configure Apache, MySQL, and PHP.
  - Deploy a sample PHP application that interacts with a MySQL database.
  - Ensure security best practices are implemented, such as securing the MySQL installation and configuring Apache for SSL.

- **Steps**
  1. **Install Apache**:
     ```bash
     sudo apt install apache2
     ```
  2. **Install MySQL**:
     ```bash
     sudo apt install mysql-server
     ```
  3. **Install PHP**:
     ```bash
     sudo apt install php php-mysql
     ```
  4. **Create a Sample PHP Application**:
     - Example `index.php`:
       ```php
       <?php
       $conn = new mysqli("localhost", "username", "password", "database");

       if ($conn->connect_error) {
           die("Connection failed: " . $conn->connect_error);
       }
       echo "Connected successfully";
       ?>
       ```
  5. **Configure Apache for SSL**:
     - Generate SSL certificates and update Apache configuration.
  6. **Test the Setup**:
     - Access the application through a web browser and verify database interactions.

## 20.3 Project 2: Node.js Application with Nginx Reverse Proxy
- **Objective**
  - Deploy a Node.js application and configure Nginx as a reverse proxy.
- **Requirements**
  - Install Node.js and npm.
  - Develop a simple Node.js application.
  - Configure Nginx to reverse proxy requests to the Node.js application.
  - Implement basic security and performance tuning for both Node.js and Nginx.

- **Steps**
  1. **Install Node.js**:
     ```bash
     sudo apt install nodejs npm
     ```
  2. **Develop a Node.js Application**:
     - Example `app.js`:
       ```javascript
       const http = require('http');
       const hostname = '127.0.0.1';
       const port = 3000;

       const server = http.createServer((req, res) => {
         res.statusCode = 200;
         res.setHeader('Content-Type', 'text/plain');
         res.end('Hello from Node.js\n');
       });

       server.listen(port, hostname, () => {
         console.log(`Server running at http://${hostname}:${port}/`);
       });
       ```
  3. **Install and Configure Nginx**:
     - Example Nginx configuration:
       ```nginx
       server {
           listen 80;
           server_name example.com;

           location / {
               proxy_pass http://localhost:3000;
               proxy_set_header Host $host;
               proxy_set_header X-Real-IP $remote_addr;
               proxy_set_header X-Forwarded-For $proxy_add_x_forwarded_for;
               proxy_set_header X-Forwarded-Proto $scheme;
           }
       }
       ```
  4. **Test the Setup**:
     - Access the Node.js application via Nginx and verify functionality.

## 20.4 Project 3: Shell Scripting Automation
- **Objective**
  - Create a set of shell scripts to automate common administrative tasks.
- **Requirements**
  - Write scripts to perform tasks such as backup, user management, and system updates.
  - Implement logging and error handling in the scripts.

- **Steps**
  1. **Backup Script**:
     - Example `backup.sh`:
       ```bash
       #!/bin/bash
       BACKUP_DIR="/var/backups"
       DATE=$(date +%F)
       BACKUP_FILE="$BACKUP_DIR/backup-$DATE.tar.gz"

       tar -czf $BACKUP_FILE /home/user/data

       if [ $? -eq 0 ]; then
           echo "Backup successful: $BACKUP_FILE" >> /var/log/backup.log
       else
           echo "Backup failed" >> /var/log/backup.log
       fi
       ```
  2. **User Management Script**:
     - Example `add_user.sh`:
       ```bash
       #!/bin/bash
       USERNAME=$1
       if id "$USERNAME" &>/dev/null; then
           echo "User $USERNAME already exists."
       else
           sudo useradd $USERNAME
           echo "User $USERNAME added successfully."
       fi
       ```
  3. **System Update Script**:
     - Example `update_system.sh`:
       ```bash
       #!/bin/bash
       sudo apt update
       sudo apt upgrade -y
       echo "System updated successfully."
       ```

## 20.5 Project 4: Security Hardening and Auditing
- **Objective**
  - Perform security hardening and auditing of a Linux server.
- **Requirements**
  - Implement security best practices such as configuring firewalls, setting up intrusion detection, and auditing system logs.
  - Document the steps taken and create a report on the security status of the server.

- **Steps**
  1. **Configure Firewall**:
     - Example with `ufw`:
       ```bash
       sudo ufw allow OpenSSH
       sudo ufw enable
       sudo ufw status
       ```
  2. **Set Up Intrusion Detection**:
     - Install and configure `fail2ban`:
       ```bash
       sudo apt install fail2ban
       sudo systemctl start fail2ban
       sudo systemctl enable fail2ban
       ```
  3. **Audit System Logs**:
     - Review logs and set up `logwatch`:
       ```bash
       sudo apt install logwatch
       logwatch --detail High --mailto you@example.com
       ```

## 20.6 Conclusion
Final projects are designed to provide hands-on experience with the skills and knowledge gained throughout the course. Successfully completing these projects will demonstrate your ability to deploy, manage, and secure various systems and applications.

- **Key Takeaways**:
  - **LAMP Stack Deployment**: Integrate Linux, Apache, MySQL, and PHP.
  - **Node.js and Nginx**: Deploy a Node.js application and configure Nginx as a reverse proxy.
  - **Shell Scripting**: Automate administrative tasks with shell scripts.
  - **Security Hardening**: Implement and audit security measures on a Linux server.

These projects will help solidify your understanding and prepare you for real-world scenarios in system administration and application management.


<a href="README.md">&laquo; main menu</a>