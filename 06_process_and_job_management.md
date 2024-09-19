# Chapter 6: Process and Job Management

## 6.1 Introduction to Processes in Linux
- **What is a Process?**:
  - A process is an instance of a running program. Every process in Linux is assigned a unique **Process ID (PID)**.
  - Linux manages processes through a hierarchical tree, with each process having a parent (except the initial process `init` or `systemd`).
- **Foreground vs. Background Processes**:
  - **Foreground**: Processes that run directly in the terminal and interact with the user.
  - **Background**: Processes that run in the background, allowing the terminal to be used for other tasks.
  
## 6.2 Viewing Running Processes
- **`ps` Command**:
  - Displays information about active processes.
  - Example: `ps` shows processes in the current terminal session.
  - Common usage: `ps aux` provides detailed information about all running processes.
    - **a**: Shows processes for all users.
    - **u**: Displays user/owner information.
    - **x**: Includes processes without a terminal.
- **`top` Command**:
  - An interactive, real-time view of system processes, including CPU and memory usage.
  - **Key commands** in `top`:
    - `k`: Kill a process by entering its PID.
    - `r`: Renice (change priority) of a process.
    - `q`: Quit `top`.
  - **Example**: `top` gives a real-time overview of processes and resource consumption.
- **`htop` Command**:
  - Similar to `top`, but with an enhanced interface and more user-friendly features.
  - **Features**:
    - Color-coded display.
    - Allows process tree visualization.
    - Easier navigation and process management.

## 6.3 Managing Processes
- **Killing Processes**:
  - **`kill`**: Sends a signal to a process, most commonly used to terminate it.
    - Example: `kill <PID>` sends the default `SIGTERM` signal to gracefully stop a process.
    - Use `kill -9 <PID>` to forcefully kill a stubborn process (sends `SIGKILL`).
  - **`killall`**: Terminates all processes matching a specified name.
    - Example: `killall firefox` kills all instances of the Firefox browser.
- **Suspending and Resuming Processes**:
  - **Ctrl + Z**: Suspend a running process (move it to the background in a stopped state).
  - **`bg` Command**: Resume a suspended process in the background.
    - Example: After suspending a process with `Ctrl + Z`, use `bg` to resume it.
  - **`fg` Command**: Bring a background process to the foreground.
    - Example: `fg` brings the last suspended process to the foreground.
  
## 6.4 Job Control
- **What is a Job?**:
  - A job is a command or process that is started from a shell session. Jobs can run in the background or foreground.
- **Viewing Jobs**:
  - **`jobs` Command**: Lists active jobs in the current shell session.
    - Example: Running `jobs` shows jobs with their job number, state, and command.
- **Starting Jobs in the Background**:
  - Use `&` to run a command in the background.
    - Example: `sleep 60 &` runs the `sleep` command in the background for 60 seconds.
  - After a job is started in the background, its job number will be displayed (e.g., `[1] 12345`, where `12345` is the PID).
  
## 6.5 Process Priorities and Scheduling
- **Understanding Process Priority**:
  - Linux assigns priority to processes, determining how CPU time is allocated. Priorities are referred to as **niceness** values.
  - A process’s **niceness** ranges from `-20` (highest priority) to `19` (lowest priority).
- **Changing Process Priority**:
  - **`nice`**: Used to start a process with a specified niceness.
    - Example: `nice -n 10 ./script.sh` starts the script with a niceness of 10 (lower priority).
  - **`renice`**: Changes the priority of an already running process.
    - Example: `renice -n 5 -p 12345` changes the priority of the process with PID `12345` to 5.

## 6.6 Monitoring System Performance with `top` and `htop`
- **Using `top` for Performance Monitoring**:
  - Provides real-time information on system resource usage, including CPU, memory, and load average.
  - Key metrics to watch:
    - **%CPU**: Percentage of CPU usage by each process.
    - **%MEM**: Memory usage of each process.
    - **Load Average**: Averages for the number of processes waiting for CPU over the last 1, 5, and 15 minutes.
- **Using `htop` for Enhanced Monitoring**:
  - `htop` offers a more intuitive and visual representation of system resources.
  - **Interactive Commands**:
    - `F6`: Sort processes by criteria (e.g., CPU, memory usage).
    - `F9`: Kill a selected process.
    - `F5`: View process tree to see parent-child relationships between processes.

## 6.7 Scheduling Tasks with `cron` and `at`
- **Automating Tasks with `cron`**:
  - **`cron`** is used to schedule recurring tasks. It executes commands at specified intervals (e.g., daily, weekly).
  - **Crontab Syntax**:
    - A crontab entry has five fields: `minute`, `hour`, `day of month`, `month`, `day of week`, followed by the command.
    - Example: `0 2 * * * /path/to/backup.sh` runs the backup script every day at 2 AM.
  - **Managing Crontabs**:
    - **Command**: `crontab -e` opens the crontab for editing.
    - **Command**: `crontab -l` lists current cron jobs.
- **One-Time Tasks with `at`**:
  - **`at`** is used to schedule a one-time task.
    - Example: `echo "backup.sh" | at 3pm` schedules the `backup.sh` script to run at 3 PM.
  - **Managing Scheduled `at` Jobs**:
    - **Command**: `atq` lists all scheduled jobs.
    - **Command**: `atrm <job number>` removes a scheduled job.

## 6.8 Managing Daemons and Services with `systemd`
- **What is `systemd`?**:
  - `systemd` is the initialization system used by most modern Linux distributions to manage services (daemons), boot processes, and system states.
- **Managing Services**:
  - **Starting a Service**: `systemctl start <service>`.
    - Example: `systemctl start apache2` starts the Apache web server.
  - **Stopping a Service**: `systemctl stop <service>`.
    - Example: `systemctl stop apache2` stops the Apache service.
  - **Restarting a Service**: `systemctl restart <service>`.
    - Example: `systemctl restart apache2` restarts the Apache service.
  - **Checking Service Status**: `systemctl status <service>`.
    - Example: `systemctl status apache2` shows the current status of the Apache service.
- **Enabling and Disabling Services**:
  - **Enabling**: `systemctl enable <service>` configures a service to start automatically at boot.
    - Example: `systemctl enable apache2`.
  - **Disabling**: `systemctl disable <service>` prevents a service from starting automatically.
    - Example: `systemctl disable apache2`.

## 6.9 Process and Resource Limits (`ulimit`)
- **What is `ulimit`?**:
  - `ulimit` is used to limit the system resources available to the shell and its child processes (e.g., maximum number of open files, maximum memory usage).
- **Viewing and Setting Limits**:
  - **Command**: `ulimit -a` shows all resource limits for the current shell session.
  - Example: `ulimit -n` shows the maximum number of open files.
  - **Changing Limits**:
    - Example: `ulimit -n 4096` increases the maximum number of open files to 4096 for the current session.
  
## 6.10 Best Practices for Process and Job Management
- **Monitor Resource Usage**:
  - Regularly use tools like `top`, `htop`, or `ps` to monitor resource usage and identify resource-hogging processes.
- **Gracefully Terminate Processes**:
  - Always attempt to use `SIGTERM` (default signal) to stop processes before using `SIGKILL` to force termination.
- **Use Cron for Scheduled Tasks**:
  - Automate routine maintenance, backups, and other administrative tasks using `cron` for efficiency.
- **Avoid Overusing `sudo` for Process Management**:
  - Run processes as a regular user whenever possible, reserving root privileges for tasks that truly require them.
