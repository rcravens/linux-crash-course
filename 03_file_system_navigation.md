# Chapter 3: File System Navigation

## 3.1 The Linux File System Hierarchy
- **Root Directory `/`**:
  - The top-most directory in the Linux file system.
  - All files and directories are contained within `/`.
- **Standard Directories**:
  - `/bin`: Essential binaries (commands like `ls`, `cp`, `mv`).
  - `/etc`: Configuration files for system-wide settings.
  - `/home`: Home directories for users (e.g., `/home/user`).
  - `/var`: Variable files such as logs and spools.
  - `/tmp`: Temporary files, usually cleared on reboot.
  - `/usr`: User-installed software and system files.
  - `/dev`: Device files for hardware like disks and USB devices.
  - `/mnt` and `/media`: Mount points for external and removable drives.
  - `/opt`: Optional software, typically used for third-party applications.
- **Purpose of Each Directory**: Provide a brief explanation of what each major directory contains and how it is used in administration.

## 3.2 Paths: Absolute and Relative
- **Absolute Path**:
  - Begins from the root directory `/`.
  - Example: `/home/user/documents/report.txt`.
- **Relative Path**:
  - Starts from the current directory.
  - Example: If you are in `/home/user/`, `documents/report.txt` is a relative path to `report.txt`.
- **Navigating Between Directories**:
  - `..`: Refers to the parent directory.
  - `.`: Refers to the current directory.
  - Example: `cd ../` moves one directory up, while `cd ./folder/` stays within the current directory.

## 3.3 Essential Commands for File System Navigation
- **`pwd` (Print Working Directory)**:
  - Shows the full path of the current directory.
  - Example: `pwd` might output `/home/user/projects`.
- **`cd` (Change Directory)**:
  - Change the current directory to a different location.
  - Usage:
    - `cd /home/user`: Change to an absolute path.
    - `cd ..`: Move up one directory level.
    - `cd ~/documents`: Navigate to a subdirectory within the home directory using `~` (home directory shortcut).
- **`ls` (List Files)**:
  - Lists the contents of the current or specified directory.
  - Common options:
    - `ls -l`: Long listing format (shows file permissions, size, and modification date).
    - `ls -a`: Show hidden files (those starting with `.`).
    - `ls -h`: Human-readable file sizes (e.g., `KB`, `MB`).
    - `ls /etc`: Lists the contents of the `/etc` directory.
- **`tree` (Directory Tree Listing)**:
  - Displays a hierarchical view of the directory structure in a tree format.
  - Example: `tree /home/user/` shows a tree of all files and directories under `/home/user/`.

## 3.4 Hidden Files and Directories
- **Hidden Files**:
  - Files and directories starting with a dot (`.`) are considered hidden.
  - Example: `.bashrc` or `.ssh/`.
- **Viewing Hidden Files**:
  - Use the `ls -a` command to see hidden files and directories.
  - Example: `ls -la` for a detailed listing of all files, including hidden ones.
  
## 3.5 Understanding File Permissions
- **Basic Permissions Structure**:
  - Each file and directory has three permission sets:
    - **User** (owner): Permissions for the file's owner.
    - **Group**: Permissions for a specific user group.
    - **Others**: Permissions for all other users.
- **Permission Types**:
  - **Read (`r`)**: Ability to read the file or list directory contents.
  - **Write (`w`)**: Ability to modify the file or directory contents.
  - **Execute (`x`)**: Ability to run a file (execute scripts or binaries) or enter a directory.
- **Viewing Permissions**:
  - Use the `ls -l` command to view permissions.
  - Example: 
    ```
    -rwxr-xr--
    ```
    This means:
    - The owner can read, write, and execute (`rwx`).
    - The group can read and execute (`r-x`).
    - Others can only read (`r--`).

## 3.6 Modifying File Permissions and Ownership
- **`chmod` (Change Mode)**:
  - Used to change file permissions.
  - Syntax:
    - **Numeric Method**: Assigns permissions using numeric values (e.g., `chmod 755 file`).
      - 4 = read, 2 = write, 1 = execute.
      - Example: `chmod 755` sets `rwxr-xr-x` permissions.
    - **Symbolic Method**: Modifies permissions using symbols (e.g., `chmod u+x file`).
      - `u`: User (owner), `g`: Group, `o`: Others.
      - `+`: Add permission, `-`: Remove permission.
      - Example: `chmod g+w file` adds write permission for the group.
- **`chown` (Change Ownership)**:
  - Change the ownership of files or directories.
  - Syntax: `chown <owner>:<group> <file>` (e.g., `chown user:staff file.txt`).
  - Example: `chown user:usergroup example.txt` changes ownership of `example.txt` to `user` and the group to `usergroup`.

## 3.7 Understanding Symbolic Links and Hard Links
- **Symbolic (Soft) Links**:
  - A symbolic link is a pointer to another file or directory.
  - Example: `ln -s /home/user/file.txt shortcut.txt` creates a symbolic link `shortcut.txt` that points to `file.txt`.
  - Useful for linking to files in other directories without duplicating the file itself.
- **Hard Links**:
  - A hard link creates another file that points to the same data on the disk.
  - Both the original file and the hard link point to the same inode.
  - Example: `ln /home/user/file.txt file_link.txt`.
- **Differences**:
  - Symbolic links can point to directories, hard links cannot.
  - Hard links remain valid even if the original file is deleted, whereas symbolic links will break.

## 3.8 File and Directory Size
- **Checking Directory Sizes**:
  - `du` (Disk Usage): Summarizes disk usage of files and directories.
  - Example: `du -sh /home/user/` shows the total size of `/home/user/` in human-readable format.
- **Checking Free Disk Space**:
  - `df`: Displays available disk space on mounted file systems.
  - Example: `df -h` shows free and used disk space in human-readable format.

## 3.9 Finding Files and Directories
- **`find`**:
  - Search for files and directories based on various criteria such as name, type, or permissions.
  - Syntax: `find <path> -name <filename>`.
  - Example: `find /home/user/ -name "file.txt"` searches for `file.txt` in `/home/user/`.
- **`locate`**:
  - A faster search tool that uses an index to locate files.
  - Example: `locate file.txt` quickly finds the location of `file.txt`.
- **`which`**:
  - Finds the location of executable programs.
  - Example: `which python` shows the path to the Python executable.

## 3.10 Best Practices for File System Navigation
- **Organize Your Files**:
  - Keep your home directory clean and structured (e.g., using `Documents`, `Downloads`, `Projects`).
- **Use Autocompletion**:
  - Leverage the `Tab` key to autocomplete file paths and commands.
- **Know Where You Are**:
  - Regularly use `pwd` to ensure you're in the correct directory.
- **Be Careful with `rm`**:
  - Use `rm` cautiously, especially with `-r` (recursive) or `-f` (force) flags.
  - Always double-check the file path before deleting anything.
