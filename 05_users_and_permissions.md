# Chapter 5: Users and Permissions

<a href="README.md">&laquo; main menu</a>

## 5.1 Introduction to Users in Linux
- **User Accounts**:
  - Linux is a multi-user system, meaning multiple users can operate independently on the same machine.
  - Each user account is identified by a unique **UID** (User ID).
- **Types of Users**:
  - **Root User**: The superuser with full access to all system resources and permissions. The root user can perform any administrative task.
  - **Regular Users**: Standard user accounts with restricted access to system files and resources.
  - **System Users**: Accounts used by the system or applications to run services (e.g., `www-data` for web servers).
- **Home Directory**:
  - Every regular user has a home directory under `/home/` (e.g., `/home/bob/`).
  - The home directory is where user-specific files and configurations are stored.
  
## 5.2 Understanding Groups
- **What are Groups?**:
  - Groups in Linux are a way to assign permissions to multiple users simultaneously.
  - Each group is identified by a **GID** (Group ID).
- **Primary and Secondary Groups**:
  - **Primary Group**: The default group associated with a user.
  - **Secondary Groups**: Additional groups a user can belong to for extra permissions.
- **Common Groups**:
  - **sudo**: Users in this group can execute administrative commands with elevated privileges.
  - **wheel** (on some distributions): Similar to the `sudo` group, users in this group can perform administrative tasks.

## 5.3 Adding and Managing Users
- **Creating a New User**:
  - **Command**: `useradd <username>`.
  - Example: `useradd alice` creates a new user named `alice`.
  - **Creating a User with a Home Directory**:
    - `useradd -m <username>` creates a home directory for the user.
    - Example: `useradd -m bob` creates `/home/bob/`.
- **Setting a Password**:
  - **Command**: `passwd <username>`.
  - Example: `passwd alice` sets the password for the user `alice`.
- **Changing User Details**:
  - **Command**: `usermod` is used to modify user attributes.
  - Example: `usermod -aG sudo alice` adds `alice` to the `sudo` group (giving administrative privileges).
- **Deleting a User**:
  - **Command**: `userdel <username>`.
  - Example: `userdel bob` deletes the user `bob`.
  - To delete the user and their home directory: `userdel -r bob`.

## 5.4 Adding and Managing Groups
- **Creating a Group**:
  - **Command**: `groupadd <groupname>`.
  - Example: `groupadd developers` creates a group called `developers`.
- **Adding a User to a Group**:
  - **Command**: `usermod -aG <groupname> <username>`.
  - Example: `usermod -aG developers alice` adds the user `alice` to the `developers` group.
- **Viewing Group Membership**:
  - **Command**: `groups <username>`.
  - Example: `groups alice` shows all groups that `alice` is a member of.
  
## 5.5 File Permissions in Linux
- **Permission Structure**:
  - Every file and directory in Linux has an associated owner, group, and permissions.
  - The permission string looks like `-rwxr-xr--`:
    - **User (Owner)**: `rwx` (read, write, execute).
    - **Group**: `r-x` (read, execute).
    - **Others**: `r--` (read).
- **Types of Permissions**:
  - **Read (`r`)**: Allows reading the contents of a file or listing directory contents.
  - **Write (`w`)**: Allows modifying a file or adding/removing files in a directory.
  - **Execute (`x`)**: Allows executing a file (for scripts or binaries) or entering a directory.

## 5.6 Changing File Permissions
- **Viewing File Permissions**:
  - **Command**: `ls -l` lists files and their permissions.
  - Example: `ls -l /home/alice/file.txt` might output `-rw-r--r--`, showing the file's permissions.
- **Changing Permissions with `chmod`**:
  - **Symbolic Method**: Use letters to represent permissions (e.g., `u`, `g`, `o` for user, group, others).
    - Example: `chmod u+x file.sh` gives the owner execute permission for `file.sh`.
  - **Numeric Method**: Use octal numbers (4 = read, 2 = write, 1 = execute).
    - Example: `chmod 755 file.sh` sets the permission to `rwxr-xr-x`.
  - Common Octal Permission Codes:
    - `755`: User can read, write, execute; group and others can read and execute.
    - `644`: User can read and write; group and others can only read.
  
## 5.7 Changing Ownership of Files and Directories
- **Viewing Ownership**:
  - Use `ls -l` to view the owner and group of a file.
  - Example: `ls -l file.txt` shows `bob bob`, meaning `bob` owns the file and it's in the `bob` group.
- **Changing Ownership with `chown`**:
  - **Command**: `chown <user>:<group> <file>`.
  - Example: `chown alice:developers file.txt` changes the ownership of `file.txt` to user `alice` and group `developers`.
- **Changing Group Ownership with `chgrp`**:
  - **Command**: `chgrp <groupname> <file>`.
  - Example: `chgrp staff file.txt` changes the group ownership to `staff`.
  
## 5.8 Special Permissions (Setuid, Setgid, Sticky Bit)
- **Setuid**:
  - If set on a file, allows users to execute the file with the file owner's privileges.
  - Example: `chmod u+s /path/to/file` sets the Setuid bit on a file.
- **Setgid**:
  - When set on a directory, new files created within the directory inherit the group ownership.
  - Example: `chmod g+s /path/to/directory`.
- **Sticky Bit**:
  - When set on a directory, only the owner of a file can delete it, even if others have write permissions.
  - Example: `chmod +t /path/to/directory`.
  - Commonly used on `/tmp` to prevent users from deleting other users' temporary files.

## 5.9 Sudo and Root Privileges
- **Using `sudo` for Administrative Tasks**:
  - The `sudo` command allows permitted users to execute commands as the root user.
  - Example: `sudo apt update` runs the `apt update` command with root privileges.
- **Switching to the Root User**:
  - **Command**: `su` or `sudo su` to switch to the root user.
  - Example: `su -` or `sudo su -` switches to the root user with the root environment loaded.
- **Best Practices for `sudo`**:
  - Avoid using `sudo` for every command. Use it only when necessary.
  - Always verify commands before running them with root privileges to avoid damaging the system.

## 5.10 Managing Sudo Privileges
- **Editing the `sudoers` File**:
  - The `sudoers` file controls which users can execute `sudo` and what commands they can run.
  - Always edit this file using `visudo` to prevent syntax errors.
  - Example: Add a user to the `sudoers` file by adding `alice ALL=(ALL:ALL) ALL`, allowing `alice` to run any command as any user.
- **Adding Users to the `sudo` Group**:
  - **Command**: `usermod -aG sudo <username>`.
  - Example: `usermod -aG sudo alice` gives `alice` sudo privileges.

## 5.11 Best Practices for User and Permission Management
- **Least Privilege Principle**:
  - Always assign the minimal permissions needed for a user or group to perform their tasks.
  - Avoid giving regular users unnecessary sudo access.
- **Regularly Audit Permissions**:
  - Periodically check file permissions and group memberships to ensure they align with current security needs.
- **Locking and Unlocking User Accounts**:
  - **Lock**: Use `passwd -l <username>` to lock a user account.
  - **Unlock**: Use `passwd -u <username>` to unlock an account.
- **Temporary Users**:
  - Use tools like `adduser --expiredate` to set expiration dates for temporary accounts, ensuring they are automatically disabled after a specific time.

<a href="README.md">&laquo; main menu</a>