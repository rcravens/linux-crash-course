# Chapter 13: Security Basics

<a href="README.md">&laquo; main menu</a>

## 13.1 Introduction to Security in Linux
- **Purpose**
  - Ensure the security and integrity of the Linux system by implementing best practices and understanding potential threats.
  - Focus on user management, permissions, and system hardening.

## 13.2 User Management and Access Control
- **Creating and Managing Users**
  - **Add a User**:
    ```bash
    sudo adduser username
    ```
  - **Delete a User**:
    ```bash
    sudo deluser username
    ```
  - **Modify User Information**:
    ```bash
    sudo usermod -aG groupname username
    ```
  - **Explanation**: Adds a user to a group, which can help manage permissions.

- **Managing User Groups**
  - **Create a Group**:
    ```bash
    sudo addgroup groupname
    ```
  - **Delete a Group**:
    ```bash
    sudo delgroup groupname
    ```
  - **Add User to Group**:
    ```bash
    sudo usermod -aG groupname username
    ```

## 13.3 File and Directory Permissions
- **Understanding Permissions**
  - **Permission Types**:
    - `r` (read)
    - `w` (write)
    - `x` (execute)
  - **Permission Representation**:
    ```bash
    rwxr-xr-x
    ```
  - **Explanation**: Represents permissions for owner, group, and others.

- **Changing Permissions**
  - **Using `chmod`**:
    ```bash
    chmod 755 filename
    ```
  - **Explanation**: Sets permissions to `rwxr-xr-x` for the file.
  - **Octal vs. Symbolic Notation**:
    - Octal: `755`
    - Symbolic: `u=rwx,g=rx,o=rx`

- **Changing Ownership**
  - **Using `chown`**:
    ```bash
    sudo chown owner:group filename
    ```
  - **Explanation**: Changes the owner and group of the file.

## 13.4 Securing SSH
- **Configuring SSH**
  - **Edit SSH Configuration**:
    ```bash
    sudo nano /etc/ssh/sshd_config
    ```
  - **Important Settings**:
    - **Disable Root Login**:
      ```bash
      PermitRootLogin no
      ```
    - **Change Default Port**:
      ```bash
      Port 2222
      ```
    - **Explanation**: Enhances security by reducing the risk of automated attacks.

- **Using SSH Keys**
  - **Generate SSH Key Pair**:
    ```bash
    ssh-keygen -t rsa
    ```
  - **Copy Public Key to Server**:
    ```bash
    ssh-copy-id user@hostname
    ```
  - **Explanation**: SSH keys provide a more secure authentication method compared to passwords.

## 13.5 Firewall Basics
- **Using `ufw` (Uncomplicated Firewall)**
  - **Enable UFW**:
    ```bash
    sudo ufw enable
    ```
  - **Allow Specific Port**:
    ```bash
    sudo ufw allow 22
    ```
  - **Deny Specific Port**:
    ```bash
    sudo ufw deny 80
    ```
  - **Check Status**:
    ```bash
    sudo ufw status
    ```
  - **Explanation**: `ufw` simplifies firewall management and configuration.

## 13.6 System Hardening
- **Updating Software**
  - **Update Package List**:
    ```bash
    sudo apt update
    ```
  - **Upgrade Installed Packages**:
    ```bash
    sudo apt upgrade
    ```
  - **Explanation**: Regular updates ensure that security patches and bug fixes are applied.

- **Configuring Security Settings**
  - **Disable Unnecessary Services**:
    ```bash
    sudo systemctl stop service
    sudo systemctl disable service
    ```
  - **Explanation**: Reduces the attack surface by disabling services that are not needed.

## 13.7 Monitoring and Auditing
- **Using `auditd`**
  - **Install Auditd**:
    ```bash
    sudo apt install auditd
    ```
  - **Configure Audit Rules**:
    ```bash
    sudo nano /etc/audit/audit.rules
    ```
  - **Check Audit Logs**:
    ```bash
    sudo ausearch -m avc
    ```
  - **Explanation**: `auditd` provides detailed logs of system activities and security events.

- **Using `logwatch`**
  - **Install Logwatch**:
    ```bash
    sudo apt install logwatch
    ```
  - **Generate Report**:
    ```bash
    sudo logwatch --detail high --mailto your-email@example.com
    ```
  - **Explanation**: `logwatch` helps in monitoring and analyzing system logs.

## 13.8 Conclusion
Understanding and implementing basic security practices is crucial for maintaining a secure Linux environment. By managing users, configuring permissions, securing SSH, using firewalls, and monitoring system activity, you can significantly improve the security of your system.

- **Key Takeaways**:
  - **User Management**: Properly manage users and groups.
  - **Permissions**: Set and modify file and directory permissions.
  - **SSH Security**: Configure and secure SSH access.
  - **Firewall**: Use `ufw` to manage network traffic.
  - **System Hardening**: Keep software updated and disable unnecessary services.
  - **Monitoring**: Regularly audit and monitor system logs.

Continue applying these security practices and stay informed about new threats and best practices to maintain a secure Linux system.

<a href="README.md">&laquo; main menu</a>