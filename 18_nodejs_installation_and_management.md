# Chapter 18: Node.js Installation and Management

## 18.1 Introduction to Node.js
- **Purpose**
  - Node.js is a JavaScript runtime built on Chrome's V8 JavaScript engine. It allows developers to build scalable network applications using JavaScript on the server side.
  - It is known for its non-blocking, event-driven architecture, which makes it suitable for building real-time applications.

## 18.2 Installing Node.js
- **On Debian/Ubuntu**
  - **Update Package Index**:
    ```bash
    sudo apt update
    ```
  - **Install Node.js Using NodeSource Repository**:
    - **Add NodeSource Repository**:
      ```bash
      curl -fsSL https://deb.nodesource.com/setup_18.x | sudo -E bash -
      ```
    - **Install Node.js**:
      ```bash
      sudo apt install -y nodejs
      ```
    - **Install Build Tools (Optional)**:
      ```bash
      sudo apt install -y build-essential
      ```
    - **Explanation**: The NodeSource repository provides the latest Node.js packages. `build-essential` is required for compiling native addons.

- **On CentOS/RHEL**
  - **Add NodeSource Repository**:
    ```bash
    curl -fsSL https://rpm.nodesource.com/setup_18.x | sudo bash -
    ```
  - **Install Node.js**:
    ```bash
    sudo yum install -y nodejs
    ```
  - **Install Build Tools (Optional)**:
    ```bash
    sudo yum groupinstall -y "Development Tools"
    ```

- **Using NVM (Node Version Manager)**
  - **Install NVM**:
    ```bash
    curl -o- https://raw.githubusercontent.com/nvm-sh/nvm/v0.39.5/install.sh | bash
    ```
  - **Load NVM**:
    ```bash
    export NVM_DIR="$HOME/.nvm"
    [ -s "$NVM_DIR/nvm.sh" ] && \. "$NVM_DIR/nvm.sh"
    ```
  - **Install Node.js**:
    ```bash
    nvm install 18
    ```
  - **Set Default Node Version**:
    ```bash
    nvm alias default 18
    ```

## 18.3 Basic Node.js Usage
- **Check Node.js and npm Versions**
  - **Node.js Version**:
    ```bash
    node -v
    ```
  - **npm Version**:
    ```bash
    npm -v
    ```

- **Creating a Simple Node.js Application**
  - **Example Application**:
    - **Create `app.js`**:
      ```javascript
      const http = require('http');

      const hostname = '127.0.0.1';
      const port = 3000;

      const server = http.createServer((req, res) => {
        res.statusCode = 200;
        res.setHeader('Content-Type', 'text/plain');
        res.end('Hello World\n');
      });

      server.listen(port, hostname, () => {
        console.log(`Server running at http://${hostname}:${port}/`);
      });
      ```
    - **Run the Application**:
      ```bash
      node app.js
      ```

- **Installing and Using npm Packages**
  - **Install a Package**:
    ```bash
    npm install <package-name>
    ```
  - **Example**:
    ```bash
    npm install express
    ```
  - **Use the Package in Code**:
    ```javascript
    const express = require('express');
    const app = express();

    app.get('/', (req, res) => {
      res.send('Hello World!');
    });

    app.listen(3000, () => {
      console.log('Example app listening on port 3000!');
    });
    ```

## 18.4 Managing Node.js Applications
- **Using `pm2` for Process Management**
  - **Install pm2**:
    ```bash
    sudo npm install -g pm2
    ```
  - **Start Application with pm2**:
    ```bash
    pm2 start app.js
    ```
  - **View pm2 Status**:
    ```bash
    pm2 status
    ```
  - **Restart and Stop Applications**:
    ```bash
    pm2 restart app.js
    pm2 stop app.js
    ```
  - **Save Process List**:
    ```bash
    pm2 save
    ```

- **Setting Up pm2 to Start on Boot**
  - **Generate Startup Script**:
    ```bash
    pm2 startup
    ```
  - **Save Configuration**:
    ```bash
    pm2 save
    ```

## 18.5 Updating Node.js
- **Using NodeSource Repository**
  - **Update Node.js**:
    ```bash
    sudo apt update
    sudo apt upgrade -y nodejs  # Debian/Ubuntu
    sudo yum update -y nodejs    # CentOS/RHEL
    ```

- **Using NVM**
  - **Update Node.js**:
    ```bash
    nvm install <latest-version>
    nvm use <latest-version>
    ```

## 18.6 Securing Node.js Applications
- **Environment Variables**
  - **Example of Setting Environment Variables**:
    ```bash
    export NODE_ENV=production
    ```
  - **Access Environment Variables in Code**:
    ```javascript
    const environment = process.env.NODE_ENV || 'development';
    ```

- **Implementing Basic Security Practices**
  - **Sanitize Input**: Always sanitize user input to avoid SQL injection and other attacks.
  - **Use HTTPS**: Ensure communication is secured using HTTPS.

## 18.7 Conclusion
Node.js is a powerful runtime for building scalable and high-performance applications. By mastering installation, basic usage, process management, and security practices, you can effectively manage and deploy Node.js applications.

- **Key Takeaways**:
  - **Installation**: Install Node.js using NodeSource, NVM, or native package managers.
  - **Basic Usage**: Create and run simple Node.js applications, and use npm for package management.
  - **Management**: Utilize `pm2` for process management and set up automatic start on boot.
  - **Updating and Securing**: Keep Node.js up-to-date and follow best security practices.

Regularly review and update your Node.js environment to ensure optimal performance and security.
