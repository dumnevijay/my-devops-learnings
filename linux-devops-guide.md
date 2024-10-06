# Linux for DevOps: A Comprehensive Guide

## Table of Contents
1. [Introduction](#introduction)
2. [Basic Linux Commands](#basic-linux-commands)
3. [File System Management](#file-system-management)
4. [User and Permission Management](#user-and-permission-management)
5. [Process Management](#process-management)
6. [System Monitoring](#system-monitoring)
7. [Networking](#networking)
8. [Shell Scripting](#shell-scripting)
9. [Package Management](#package-management)
10. [System Services](#system-services)
11. [Logs and Troubleshooting](#logs-and-troubleshooting)
12. [Security Best Practices](#security-best-practices)
13. [Advanced Topics](#advanced-topics)

## Introduction
Linux is the foundation of most DevOps tools and practices. This guide covers essential Linux concepts and commands that every DevOps engineer should know.

### Why Linux for DevOps?
- Open-source and highly customizable
- Powers most web servers and cloud instances
- Excellent tooling for automation and scripting
- Native support for containers and virtualization

## Basic Linux Commands

### Navigation and File Operations
```bash
# Directory navigation
pwd                 # Print working directory
ls -la              # List all files including hidden files
cd /path/to/dir     # Change directory
cd ..               # Move up one directory

# File operations
touch file.txt      # Create empty file
cp source dest      # Copy file
mv old new          # Move/rename file
rm file.txt         # Remove file
rm -r directory     # Remove directory and contents

# Viewing file content
cat file.txt        # Display entire file
less file.txt       # View file with pagination
head -n 10 file.txt # View first 10 lines
tail -f log.txt     # View and follow file end
```

### Text Processing
```bash
# Search within files
grep "pattern" file.txt
grep -r "pattern" /path/to/dir

# Text manipulation
sed 's/old/new/g' file.txt    # Replace text
awk '{print $1}' file.txt     # Print first column

# Word, line counting
wc -l file.txt                # Count lines
wc -w file.txt                # Count words
```

## File System Management

### Directory Structure
```
/                   # Root directory
├── bin             # User binaries
├── boot            # Boot loader files
├── dev             # Device files
├── etc             # System configuration
├── home            # User home directories
├── lib             # System libraries
├── opt             # Optional applications
├── proc            # Process information
├── root            # Root user home directory
├── tmp             # Temporary files
├── usr             # User programs
└── var             # Variable data (logs, etc.)
```

### Disk Management
```bash
# Disk usage
df -h               # Show disk space usage
du -sh /path        # Show directory size

# Mount management
mount               # List mounted filesystems
mount /dev/sdb1 /mnt/disk  # Mount a disk
umount /mnt/disk    # Unmount a disk

# File system operations
fdisk -l            # List disk partitions
mkfs.ext4 /dev/sdb1 # Create ext4 filesystem
```

## User and Permission Management

### User Operations
```bash
# User management
useradd username    # Create new user
usermod -aG group user  # Add user to group
userdel username    # Delete user

# Switch user
su - username       # Switch to user
sudo command        # Run command as root

# View user info
id username         # Show user ID and groups
who                 # Show logged in users
```

### File Permissions
```bash
# Change permissions
chmod 755 file.txt  # Change file permissions
chmod u+x script.sh # Add execute permission for user

# Change ownership
chown user:group file.txt  # Change file owner and group

# Special permissions
chmod 4755 file     # Set SUID bit
chmod 2755 file     # Set SGID bit
chmod 1755 file     # Set sticky bit
```

## Process Management

### Process Commands
```bash
# View processes
ps aux              # Show all processes
top                 # Interactive process viewer
htop                # Enhanced version of top

# Process control
kill PID            # Terminate process by ID
killall processname # Terminate process by name
nice -n 10 command  # Run with lower priority
renice 10 PID       # Change process priority

# Background processes
command &           # Run in background
nohup command &     # Run immune to hangups
jobs                # List background jobs
fg %1               # Bring job to foreground
```

## System Monitoring

### System Information
```bash
# System resources
free -h             # Show memory usage
uptime              # Show system uptime
lscpu               # Show CPU information
vmstat              # Virtual memory statistics

# Real-time monitoring
sar                 # System activity reporter
iostat              # IO statistics
netstat             # Network statistics
```

### Performance Tuning
```bash
# System limits
ulimit -a           # Show all limits
ulimit -n 4096      # Set file descriptor limit

# Process priorities
nice -n 10 command  # Run with adjusted priority
renice 10 -p PID    # Adjust running process priority

# Memory management
sync                # Flush file system buffers
sysctl -a           # Show all kernel parameters
```

## Networking

### Network Configuration
```bash
# Network interfaces
ip addr             # Show IP addresses
ip link set eth0 up # Enable interface
ifconfig            # (legacy) Show interfaces

# DNS
host example.com    # DNS lookup
dig example.com     # Detailed DNS lookup
```

### Network Troubleshooting
```bash
# Connectivity tests
ping host           # Test reachability
traceroute host     # Show route to host
mtr host            # Combine ping and traceroute

# Port checking
netstat -tulpn      # Show listening ports
ss -tulpn           # Socket statistics
lsof -i :80         # Show process using port 80

# Packet capture
tcpdump -i eth0     # Capture on interface
```

## Shell Scripting

### Basic Script Structure
```bash
#!/bin/bash

# Variables
NAME="DevOps"
echo "Hello, $NAME!"

# Control structures
if [ "$NAME" == "DevOps" ]; then
    echo "Name matches"
fi

# Loops
for i in {1..5}; do
    echo "Iteration $i"
done

# Functions
greeting() {
    echo "Hello, $1!"
}
greeting "World"
```

### Common Script Operations
```bash
# Command substitution
current_date=$(date +%Y-%m-%d)

# Arithmetic
result=$((5 + 3))

# Reading input
read -p "Enter your name: " user_name

# Exit codes
exit 0  # Success
exit 1  # Failure
```

## Package Management

### APT (Debian/Ubuntu)
```bash
# Package management
apt update              # Update package list
apt install package    # Install package
apt remove package     # Remove package
apt search keyword     # Search for package

# System upgrade
apt upgrade            # Upgrade packages
apt dist-upgrade       # Smart upgrade
```

### YUM/DNF (RHEL/CentOS)
```bash
# Package management
yum install package    # Install package
yum remove package     # Remove package
yum search keyword     # Search for package

# System upgrade
yum update            # Update packages
```

## System Services

### Systemd Service Management
```bash
# Service control
systemctl start service
systemctl stop service
systemctl restart service
systemctl status service

# Service configuration
systemctl enable service   # Start on boot
systemctl disable service  # Don't start on boot

# View logs
journalctl -u service     # View service logs
```

### Creating a System Service
```ini
# /etc/systemd/system/myapp.service
[Unit]
Description=My Application
After=network.target

[Service]
Type=simple
User=myapp
WorkingDirectory=/opt/myapp
ExecStart=/usr/bin/python3 app.py
Restart=always

[Install]
WantedBy=multi-user.target
```

## Logs and Troubleshooting

### System Logs
```bash
# View logs
tail -f /var/log/syslog    # Follow system log
journalctl                 # View systemd logs
journalctl -f              # Follow systemd logs

# Log rotation
logrotate                  # Rotate log files
cat /etc/logrotate.conf    # Log rotation config
```

### Troubleshooting Tools
```bash
# System troubleshooting
dmesg                      # Kernel ring buffer
strace command             # Trace system calls
lsof                       # List open files

# Performance issues
top                        # System monitor
iotop                      # I/O monitor
vmstat                     # Virtual memory stats
```

## Security Best Practices

### SSH Configuration
```bash
# Key-based authentication
ssh-keygen -t ed25519      # Generate SSH key
ssh-copy-id user@host      # Copy key to server

# SSH hardening
# /etc/ssh/sshd_config
PermitRootLogin no
PasswordAuthentication no
UsePAM yes
```

### Firewall Configuration
```bash
# UFW (Uncomplicated Firewall)
ufw enable                 # Enable firewall
ufw allow 22/tcp           # Allow SSH
ufw status                 # Check status

# iptables
iptables -L                # List rules
iptables -A INPUT -p tcp --dport 80 -j ACCEPT
```

## Advanced Topics

### Container Management
```bash
# Docker basics
docker ps                  # List containers
docker images              # List images
docker run image           # Run container
docker build -t name .     # Build image

# Docker Compose
docker-compose up -d       # Start services
docker-compose down        # Stop services
```

### Automation Tools
```bash
# Ansible
ansible all -m ping        # Ping hosts
ansible-playbook play.yml  # Run playbook

# Terraform
terraform init             # Initialize
terraform plan             # Show changes
terraform apply            # Apply changes
```

## Contributing
Feel free to contribute to this guide by:
1. Creating issues for corrections or additions
2. Submitting pull requests with improvements
3. Sharing your own experiences and best practices

## License
This guide is licensed under the MIT License. See [LICENSE](LICENSE) for details.

---

## Additional Resources
- [Linux Documentation Project](https://tldp.org/)
- [Linux Journey](https://linuxjourney.com/)
- [Arch Linux Wiki](https://wiki.archlinux.org/)
- [DevOps Bootcamp](https://devopsbootcamp.osuosl.org/)

## Practice Environments
- [Katacoda](https://www.katacoda.com/)
- [Play with Docker](https://labs.play-with-docker.com/)
- [Linux Survival](https://linuxsurvival.com/)

---

Remember to star this repository if you find it helpful! ⭐

Last updated: October 2024
