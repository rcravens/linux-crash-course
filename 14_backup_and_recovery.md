# Chapter 14: Backup and Recovery

<a href="README.md">&laquo; main menu</a>

## 14.1 Introduction to Backup and Recovery
- **Purpose**
  - Ensure data integrity and availability by implementing effective backup and recovery strategies.
  - Focus on creating backups, restoring data, and automating backup processes.

## 14.2 Backup Strategies
- **Types of Backups**
  - **Full Backup**:
    - Backs up all data and files.
    - **Example**: 
      ```bash
      tar -cvpzf full_backup.tar.gz /path/to/data
      ```
    - **Explanation**: Creates a compressed archive of the entire directory `/path/to/data`.
  - **Incremental Backup**:
    - Backs up only the data that has changed since the last backup.
    - **Example**:
      ```bash
      rsync -av --link-dest=/previous/backup /source/ /destination/incremental/
      ```
    - **Explanation**: Uses `rsync` to back up changed files, linking to the previous backup to save space.
  - **Differential Backup**:
    - Backs up all changes made since the last full backup.
    - **Example**:
      ```bash
      rsync -av --compare-dest=/last/full/backup /source/ /destination/differential/
      ```
    - **Explanation**: Uses `rsync` to back up changes since the last full backup.

- **Backup Scheduling**
  - **Using `cron`**:
    - **Schedule Full Backup**:
      ```bash
      0 2 * * 7 tar -cvpzf /backup/full_backup_$(date +\%F).tar.gz /path/to/data
      ```
    - **Schedule Incremental Backup**:
      ```bash
      0 3 * * * rsync -av --link-dest=/previous/backup /source/ /destination/incremental/
      ```
    - **Explanation**: Schedules backups using `cron`, with full backups weekly and incremental backups daily.

## 14.3 Recovery Procedures
- **Restoring from Backup**
  - **Full Backup Restoration**:
    - **Example**:
      ```bash
      tar -xvpzf full_backup.tar.gz -C /restore/path
      ```
    - **Explanation**: Extracts files from the `full_backup.tar.gz` archive to `/restore/path`.
  - **Incremental Backup Restoration**:
    - **Example**:
      ```bash
      rsync -av /destination/incremental/ /restore/path/
      ```
    - **Explanation**: Restores files from the incremental backup to `/restore/path`.

- **Testing Backups**
  - **Verify Backup Integrity**:
    ```bash
    tar -tvf full_backup.tar.gz
    ```
  - **Explanation**: Lists the contents of the backup archive to verify that files are present and the archive is not corrupted.

## 14.4 Backup Automation
- **Automating Backups with `cron`**
  - **Setting Up `cron` Jobs**:
    - **Edit `crontab`**:
      ```bash
      crontab -e
      ```
    - **Add Backup Jobs**:
      ```bash
      0 2 * * 1 tar -cvpzf /backup/full_backup_$(date +\%F).tar.gz /path/to/data
      ```
    - **Explanation**: Adds a job to `crontab` to perform automated backups.

- **Using Backup Tools**
  - **`rsnapshot`**:
    - **Installation**:
      ```bash
      sudo apt install rsnapshot
      ```
    - **Configuration**:
      - Edit `/etc/rsnapshot.conf` to set backup intervals and directories.
    - **Running `rsnapshot`**:
      ```bash
      sudo rsnapshot daily
      ```
    - **Explanation**: `rsnapshot` automates backups using configuration files to manage schedules and retention.

## 14.5 Backup Best Practices
- **Regular Backups**
  - **Schedule Frequent Backups**: Ensure backups are taken regularly based on data importance and change frequency.
- **Offsite Storage**
  - **Remote Backups**: Store backups offsite to protect against local disasters.
  - **Cloud Backup Solutions**: Consider using cloud services for remote backup storage.
- **Encryption and Security**
  - **Encrypt Backups**:
    ```bash
    tar -cvpzf - /path/to/data | gpg -c > backup.tar.gz.gpg
    ```
  - **Explanation**: Encrypts the backup archive using `gpg` for added security.

## 14.6 Conclusion
Effective backup and recovery strategies are critical for protecting data and ensuring business continuity. By understanding backup types, implementing recovery procedures, and automating backup processes, you can safeguard your data against loss and minimize downtime.

- **Key Takeaways**:
  - **Backup Types**: Understand full, incremental, and differential backups.
  - **Recovery Procedures**: Know how to restore from backups and test their integrity.
  - **Automation**: Use tools and scheduling to automate backups.
  - **Best Practices**: Regularly backup, use offsite storage, and secure backups with encryption.

Regularly review and update your backup and recovery procedures to keep up with changing data needs and technological advancements.

<a href="README.md">&laquo; main menu</a>