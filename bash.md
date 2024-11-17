# Bash

Here’s a list of **useful Bash commands** for automation and tasks commonly performed by **system administrators** and **network administrators**:

***

#### **1. General System Administration**

**System Information**

*   Display system information:

    ```bash
    uname -a
    ```
*   Check disk usage:

    ```bash
    df -h
    ```
*   Check memory usage:

    ```bash
    free -h
    ```

**Process Management**

*   List running processes:

    ```bash
    ps aux
    ```
*   Kill a process:

    ```bash
    kill -9 <PID>
    ```
*   Monitor system performance in real time:

    ```bash
    top
    ```

**Service Management**

*   Start, stop, or restart a service:

    ```bash
    systemctl start <service>
    systemctl stop <service>
    systemctl restart <service>
    ```
*   Check the status of a service:

    ```bash
    systemctl status <service>
    ```

***

#### **2. File and Directory Management**

**File Operations**

*   Create a new file:

    ```bash
    touch filename.txt
    ```
*   View file contents:

    ```bash
    cat filename.txt
    ```
*   Copy a file:

    ```bash
    cp source.txt destination.txt
    ```
*   Move (or rename) a file:

    ```bash
    mv oldname.txt newname.txt
    ```

**Directory Operations**

*   Create a new directory:

    ```bash
    mkdir new_directory
    ```
*   Remove a directory:

    ```bash
    rm -r directory_name
    ```
*   List files in a directory:

    ```bash
    ls -lah
    ```

**Search Files**

*   Find files by name:

    ```bash
    find /path/to/search -name "filename.txt"
    ```
*   Search for text within files:

    ```bash
    grep -R "search_term" /path/to/directory
    ```

***

#### **3. User and Group Management**

**User Management**

*   Add a new user:

    ```bash
    sudo adduser newuser
    ```
*   Delete a user:

    ```bash
    sudo deluser username
    ```

**Group Management**

*   Add a user to a group:

    ```bash
    sudo usermod -aG groupname username
    ```
*   List groups for a user:

    ```bash
    groups username
    ```

***

#### **4. Networking**

**Network Configuration**

*   Show IP address and network interfaces:

    ```bash
    ip addr
    ```
*   Set a static IP address:

    ```bash
    sudo ip addr add 192.168.1.100/24 dev eth0
    ```
*   Add a default gateway:

    ```bash
    sudo ip route add default via 192.168.1.1
    ```

**Network Diagnostics**

*   Test network connectivity:

    ```bash
    ping -c 4 google.com
    ```
*   Display open network ports:

    ```bash
    netstat -tuln
    ```
*   Check DNS resolution:

    ```bash
    dig example.com
    ```

***

#### **5. System Monitoring and Troubleshooting**

**Disk Management**

*   Check disk space usage:

    ```bash
    df -h
    ```
*   Find large files:

    ```bash
    find / -type f -size +100M
    ```

**Log Management**

*   View system logs:

    ```bash
    sudo journalctl
    ```
*   Tail logs in real-time:

    ```bash
    tail -f /var/log/syslog
    ```

**Resource Usage**

*   Check CPU usage:

    ```bash
    mpstat
    ```
*   Monitor I/O usage:

    ```bash
    iostat
    ```

***

#### **6. Automation and Scripting**

**Basic Automation**

*   Create a script:

    ```bash
    nano script.sh
    ```
*   Example script for backup:

    ```bash
    #!/bin/bash
    tar -czf backup.tar.gz /path/to/directory
    echo "Backup completed successfully!"
    ```
*   Make the script executable:

    ```bash
    chmod +x script.sh
    ```

**Schedule Tasks with Cron**

*   Edit the crontab:

    ```bash
    crontab -e
    ```
*   Schedule a script to run daily at 2 AM:

    ```bash
    0 2 * * * /path/to/script.sh
    ```

***

#### **7. Security and Auditing**

**Firewall Management**

*   List current firewall rules:

    ```bash
    sudo iptables -L
    ```
*   Add a rule to allow SSH:

    ```bash
    sudo iptables -A INPUT -p tcp --dport 22 -j ACCEPT
    ```

**File Permissions**

*   Change ownership of a file:

    ```bash
    sudo chown user:group file.txt
    ```
*   Modify file permissions:

    ```bash
    chmod 644 file.txt
    ```

***

#### **8. Package Management**

**APT (Debian-based systems)**

*   Update package lists:

    ```bash
    sudo apt update
    ```
*   Upgrade installed packages:

    ```bash
    sudo apt upgrade
    ```
*   Install a package:

    ```bash
    sudo apt install package_name
    ```

**YUM/DNF (RHEL-based systems)**

*   Install a package:

    ```bash
    sudo yum install package_name
    ```
*   List installed packages:

    ```bash
    yum list installed
    ```

***

#### **9. Useful Shortcuts**

*   Check running kernel:

    ```bash
    uname -r
    ```
*   Count lines, words, and characters in a file:

    ```bash
    wc file.txt
    ```
*   Show disk I/O stats:

    ```bash
    iostat
    ```
*   Check uptime:

    ```bash
    uptime
    ```

***

#### **10. Networking Automation**

**Restart a Network Service**

```bash
sudo systemctl restart networking
```

**SSH Automation**

*   Automate SSH command execution:

    ```bash
    ssh user@hostname "ls /path/to/directory"
    ```

***

These Bash commands are staples for any sysadmin or network admin.
