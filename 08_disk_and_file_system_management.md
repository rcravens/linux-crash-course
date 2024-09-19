# Chapter 8: Disk and File System Management

## 8.1 Introduction to Disk and File System Management
- **What is Disk and File System Management?**
  - Disk and file system management involves handling the storage devices connected to a system and the file systems used to organize data on these devices.
  - Key tasks include partitioning disks, formatting them, and managing file systems for efficient data storage and retrieval.
- **Importance of Disk and File System Management**
  - Proper disk management ensures optimal performance, data integrity, and efficient storage utilization.
  - Administrators must understand how to allocate, format, and maintain disks and file systems to avoid data loss and ensure system stability.

## 8.2 Viewing Disk Usage and Disk Information
- **Checking Disk Usage with `df`**
  - **Command**: `df -h`
  - Displays disk space usage for mounted file systems in a human-readable format.
  - Example: `df -h` shows the available and used disk space in gigabytes or megabytes.
- **Checking Disk Usage per Directory with `du`**
  - **Command**: `du -sh <directory>`
  - Displays the total size of a directory and its contents.
  - Example: `du -sh /var/log` shows the size of the `/var/log` directory.
  - Use `du -h` for human-readable format and `-a` to include files.
- **Viewing Block Device Information with `lsblk`**
  - **Command**: `lsblk`
  - Lists information about block devices (disks, partitions, etc.) and their mount points.
  - Example: `lsblk` shows an overview of available disks, their partitions, and their sizes.

## 8.3 Managing Partitions
- **What are Partitions?**
  - A partition is a defined space on a disk that can be used to install an operating system or store data. Partitions help segment disk space for different purposes (e.g., swap, root, home).
- **Partitioning Tools**:
  - **fdisk**: A command-line utility to create, modify, and delete partitions on MBR (Master Boot Record) disks.
  - **parted**: A more advanced tool supporting both MBR and GPT (GUID Partition Table) partitions.
- **Creating a Partition with `fdisk`**:
  1. **Command**: `sudo fdisk /dev/sdX` (where `X` is the disk identifier, e.g., `sda`, `sdb`).
  2. Type `n` to create a new partition.
  3. Follow prompts to specify the size and partition number.
  4. Write the changes using `w` to apply the partition table changes.
  - Example: `sudo fdisk /dev/sda` creates and manages partitions on the first disk.
- **Viewing Partition Table with `fdisk`**:
  - **Command**: `sudo fdisk -l`
  - Lists all partitions on available disks.
  - Example: `sudo fdisk -l` shows the partition table for all connected storage devices.
- **Creating a Partition with `parted`**:
  - **Command**: `sudo parted /dev/sdX`
  - Follow the interactive steps to create partitions, supporting both MBR and GPT.

## 8.4 Formatting File Systems
- **What is File System Formatting?**
  - After partitioning, the disk must be formatted with a file system, which defines how data is stored and organized.
  - Common file systems: **ext4** (most common in Linux), **XFS**, **Btrfs**, and **FAT32** for compatibility with non-Linux systems.
- **Formatting a Partition with `mkfs`**:
  - **Command**: `sudo mkfs -t <file_system_type> /dev/sdXn` (where `Xn` is the disk and partition, e.g., `sda1`, `sdb2`).
  - Example: `sudo mkfs -t ext4 /dev/sda1` formats the first partition of `/dev/sda` with the `ext4` file system.
- **File System Types**:
  - **ext4**: The default file system for many Linux distributions.
  - **XFS**: Known for high performance in large-scale environments.
  - **FAT32/exFAT**: Used for compatibility with Windows and macOS.
  - **Btrfs**: A modern file system with advanced features like snapshots and dynamic disk resizing.

## 8.5 Mounting and Unmounting File Systems
- **What is Mounting?**
  - Mounting a file system makes it accessible to the operating system and allows the user to interact with files on that file system.
  - You must mount a disk or partition before it can be accessed.
- **Mounting a File System**:
  - **Command**: `sudo mount /dev/sdXn /mnt/<mount_point>`
  - Example: `sudo mount /dev/sda1 /mnt/data` mounts the partition `/dev/sda1` to the directory `/mnt/data`.
  - You can create a custom mount point directory using `mkdir -p /mnt/<directory>`.
- **Viewing Mounted File Systems**:
  - **Command**: `mount` or `df -h`
  - Example: `mount` lists all currently mounted file systems, while `df -h` provides disk usage information.
- **Unmounting a File System**:
  - **Command**: `sudo umount /mnt/<mount_point>`
  - Example: `sudo umount /mnt/data` unmounts the `/mnt/data` file system, making it inaccessible.
  - Always unmount file systems before removing external storage devices to prevent data loss.
  
## 8.6 Managing Swap Space
- **What is Swap Space?**
  - Swap space is a dedicated partition or file used as virtual memory when the system runs out of physical RAM.
  - It helps to prevent system crashes when memory is exhausted, although it is slower than using physical RAM.
- **Checking Swap Usage**:
  - **Command**: `swapon --show` or `free -h`
  - Example: `free -h` displays the total, used, and available swap space in a human-readable format.
- **Creating a Swap File**:
  1. **Create a swap file**: `sudo fallocate -l 2G /swapfile` (creates a 2GB swap file).
  2. **Set correct permissions**: `sudo chmod 600 /swapfile`.
  3. **Mark the file as swap space**: `sudo mkswap /swapfile`.
  4. **Enable the swap file**: `sudo swapon /swapfile`.
  5. **Make the change permanent**: Add `/swapfile swap swap defaults 0 0` to `/etc/fstab`.
- **Disabling Swap Space**:
  - **Command**: `sudo swapoff /swapfile` to temporarily disable swap.
  
## 8.7 Monitoring Disk Health and Performance
- **Checking Disk Health with `smartctl`**:
  - **Command**: `sudo smartctl -a /dev/sdX`
  - Example: `sudo smartctl -a /dev/sda` retrieves a detailed report on the health and status of the disk.
- **Monitoring Disk I/O with `iostat`**:
  - **Command**: `iostat`
  - Example: `iostat` displays CPU and I/O usage statistics for your disks, helping to identify performance bottlenecks.
- **Checking File System for Errors with `fsck`**:
  - **Command**: `sudo fsck /dev/sdXn`
  - Example: `sudo fsck /dev/sda1` checks and repairs errors on the file system of `/dev/sda1`.

## 8.8 Automating Disk Mounts with `fstab`
- **What is `fstab`?**
  - The `fstab` (file systems table) file contains information about disk partitions and file systems that should be automatically mounted during system boot.
- **Editing `fstab`**:
  - **Command**: `sudo nano /etc/fstab`
  - Each line defines a file system to be mounted, including options like mount point, file system type, and permissions.
  - Example: `/dev/sda1 /mnt/data ext4 defaults 0 0` mounts `/dev/sda1` to `/mnt/data` automatically at boot.
- **Testing `fstab` Changes**:
  - **Command**: `sudo mount -a`
  - This mounts all file systems defined in `fstab` without rebooting the system to ensure the configuration is correct.

## 8.9 Advanced File System Features
- **File System Quotas**:
  - Quotas allow administrators to limit the amount of disk space or the number of files (inodes) a user or group can use.
  - **Commands**:
    - Enable quotas: `sudo quotaon /dev/sdXn`.
    - Set user quota: `sudo edquota -u <username>`.
    - Example: `sudo edquota -u alice` sets disk usage limits for the user `alice`.
- **File System Encryption**:
  - Encrypting file systems ensures that sensitive data remains secure, even if the disk is stolen or lost.
  - Tools like `LUKS` (Linux Unified Key Setup) are commonly used for disk encryption.
  - **Command**: `cryptsetup luksFormat /dev/sdXn`
  - Encrypts the partition `/dev/sdXn` using LUKS.
  - **Command**: `cryptsetup open /dev/sdXn my_encrypted_partition`
  - Opens the encrypted partition and maps it to `/dev/mapper/my_encrypted_partition`.
  - **Command**: `mkfs.ext4 /dev/mapper/my_encrypted_partition`
  - Formats the opened partition with a file system.

## 8.10 Conclusion
Effective disk and file system management is crucial for maintaining the health and efficiency of your Linux system. By understanding how to view disk usage, manage partitions, format file systems, and use advanced features like quotas and encryption, you ensure that your system remains organized, secure, and performant. Regularly monitoring disk health and performance helps prevent issues before they impact your system, while proper configuration of `fstab` and swap space keeps your system running smoothly and efficiently.
