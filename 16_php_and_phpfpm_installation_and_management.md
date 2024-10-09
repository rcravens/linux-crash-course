# Chapter 16: PHP and PHP-FPM Installation and Management

<a href="README.md">&laquo; main menu</a>

## 16.1 Introduction to PHP and PHP-FPM
- **Purpose**
  - PHP (Hypertext Preprocessor) is a popular server-side scripting language used for web development.
  - PHP-FPM (FastCGI Process Manager) is a PHP implementation designed to handle high loads and improve performance for PHP applications.

## 16.2 Installing PHP and PHP-FPM
- **On Debian/Ubuntu**
  - **Update Package Index**:
    ```bash
    sudo apt update
    ```
  - **Install PHP and PHP-FPM**:
    ```bash
    sudo apt install php php-fpm
    ```
  - **Install Additional PHP Modules**:
    ```bash
    sudo apt install php-mysql php-xml php-mbstring
    ```
  - **Start and Enable PHP-FPM**:
    ```bash
    sudo systemctl start php7.4-fpm
    sudo systemctl enable php7.4-fpm
    ```
  - **Explanation**: Installs PHP, PHP-FPM, and commonly used PHP modules. The `php7.4-fpm` version may vary based on your distribution.

- **On CentOS/RHEL**
  - **Install EPEL Repository**:
    ```bash
    sudo yum install epel-release
    ```
  - **Install PHP and PHP-FPM**:
    ```bash
    sudo yum install php php-fpm
    ```
  - **Install Additional PHP Modules**:
    ```bash
    sudo yum install php-mysqlnd php-xml php-mbstring
    ```
  - **Start and Enable PHP-FPM**:
    ```bash
    sudo systemctl start php-fpm
    sudo systemctl enable php-fpm
    ```

## 16.3 Configuring PHP-FPM
- **Configuration File Location**
  - **Main Configuration File**:
    - `/etc/php/7.4/fpm/php-fpm.conf` (Debian/Ubuntu)
    - `/etc/php-fpm.conf` (CentOS/RHEL)
  - **Pool Configuration**:
    - `/etc/php/7.4/fpm/pool.d/www.conf` (Debian/Ubuntu)
    - `/etc/php-fpm.d/www.conf` (CentOS/RHEL)

- **Editing Pool Configuration**
  - **Example Configuration**:
    ```ini
    [www]
    user = www-data
    group = www-data
    listen = /run/php/php7.4-fpm.sock
    listen.owner = www-data
    listen.group = www-data
    listen.mode = 0660
    pm = dynamic
    pm.max_children = 5
    pm.start_servers = 2
    pm.min_spare_servers = 1
    pm.max_spare_servers = 3
    ```
  - **Explanation**:
    - **user** and **group**: Specifies the user and group under which PHP-FPM runs.
    - **listen**: Defines the socket or port PHP-FPM will listen on.
    - **pm**: Process manager settings for handling PHP processes.

- **Restart PHP-FPM**
  - **Debian/Ubuntu**:
    ```bash
    sudo systemctl restart php7.4-fpm
    ```
  - **CentOS/RHEL**:
    ```bash
    sudo systemctl restart php-fpm
    ```

## 16.4 Configuring Nginx to Use PHP-FPM
- **Edit Nginx Configuration**
  - **Configuration File Location**:
    - `/etc/nginx/sites-available/default` (Debian/Ubuntu)
    - `/etc/nginx/nginx.conf` (CentOS/RHEL)

  - **Example Configuration**:
    ```nginx
    server {
        listen 80;
        server_name example.com;

        root /var/www/html;
        index index.php index.html index.htm;

        location / {
            try_files $uri $uri/ =404;
        }

        location ~ \.php$ {
            include snippets/fastcgi-php.conf;
            fastcgi_pass unix:/run/php/php7.4-fpm.sock;
            fastcgi_param SCRIPT_FILENAME $document_root$fastcgi_script_name;
            include fastcgi_params;
        }
    }
    ```
  - **Explanation**:
    - **location ~ \.php$**: Configures Nginx to process PHP files.
    - **fastcgi_pass**: Points to the PHP-FPM socket or TCP port.

- **Testing Nginx Configuration**
  - **Syntax Check**:
    ```bash
    sudo nginx -t
    ```
  - **Reload Nginx**:
    ```bash
    sudo systemctl reload nginx
    ```

## 16.5 Managing PHP and PHP-FPM
- **PHP Version Management**
  - **Check PHP Version**:
    ```bash
    php -v
    ```
  - **Update PHP**:
    ```bash
    sudo apt update
    sudo apt upgrade php
    ```

- **PHP-FPM Process Management**
  - **View PHP-FPM Processes**:
    ```bash
    ps aux | grep php-fpm
    ```
  - **Restart PHP-FPM**:
    ```bash
    sudo systemctl restart php-fpm
    ```

## 16.6 Securing PHP
- **Disable Dangerous Functions**
  - **Edit PHP Configuration**:
    - **Configuration File Location**:
      - `/etc/php/7.4/fpm/php.ini` (Debian/Ubuntu)
      - `/etc/php.ini` (CentOS/RHEL)
    - **Disable Functions**:
      ```ini
      disable_functions = exec,passthru,shell_exec,system
      ```

- **Enable `open_basedir`**
  - **Configuration**:
    ```ini
    open_basedir = /var/www/html:/tmp
    ```
  - **Explanation**: Restricts PHP scripts to access only specified directories.

## 16.7 Conclusion
Proper installation and configuration of PHP and PHP-FPM are crucial for running PHP-based web applications efficiently and securely. By understanding installation steps, configuring PHP-FPM, integrating with Nginx, and applying security best practices, you can effectively manage a PHP environment.

- **Key Takeaways**:
  - **Installation**: Install PHP and PHP-FPM on various distributions.
  - **Configuration**: Set up PHP-FPM pools and integrate with Nginx.
  - **Management**: Manage PHP and PHP-FPM processes and versions.
  - **Security**: Implement security settings to protect your PHP environment.

Regularly review and update your PHP configuration to adapt to new features, performance improvements, and security enhancements.

<a href="README.md">&laquo; main menu</a>