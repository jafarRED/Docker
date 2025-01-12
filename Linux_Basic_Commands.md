
# Linux Commands Cheat Sheet

## 1. File and Directory Commands
| Command | Description |
|---------|-------------|
| `pwd` | Print the current working directory. |
| `ls` | List files and directories in the current directory. |
| `ls -l` | List files with detailed information (permissions, owner, size, etc.). |
| `ls -a` | List all files, including hidden ones (starting with `.`). |
| `cd <directory>` | Change the current directory. |
| `cd ..` | Go to the parent directory. |
| `cd ~` | Go to the home directory. |
| `mkdir <directory>` | Create a new directory. |
| `rmdir <directory>` | Remove an empty directory. |
| `rm <file>` | Remove a file. |
| `rm -r <directory>` | Remove a directory and its contents. |
| `touch <filename>` | Create an empty file. |
| `cp <source> <destination>` | Copy a file or directory. |
| `cp -r <source> <destination>` | Copy a directory and its contents. |
| `mv <source> <destination>` | Move or rename a file or directory. |
| `find <directory> -name <name>` | Search for files in a directory by name. |
| `locate <filename>` | Find the location of a file (uses a database). |

## 2. File Viewing and Editing
| Command | Description |
|---------|-------------|
| `cat <file>` | Display the contents of a file. |
| `tac <file>` | Display the contents of a file in reverse order. |
| `less <file>` | View the content of a file one screen at a time. |
| `more <file>` | Similar to less, but with fewer options. |
| `head <file>` | Display the first 10 lines of a file. |
| `head -n <number> <file>` | Display the first `<number>` lines of a file. |
| `tail <file>` | Display the last 10 lines of a file. |
| `tail -n <number> <file>` | Display the last `<number>` lines of a file. |
| `nano <file>` | Open the file in the Nano text editor. |
| `vi <file>` | Open the file in the Vi text editor. |
| `vim <file>` | Open the file in the Vim text editor. |

## 3. User Management
| Command | Description |
|---------|-------------|
| `whoami` | Show the current logged-in user. |
| `who` | List all users currently logged in. |
| `id` | Display user ID (UID) and group ID (GID). |
| `adduser <username>` | Add a new user. |
| `passwd <username>` | Change the password of a user. |
| `su <username>` | Switch to another user. |
| `sudo <command>` | Execute a command with superuser privileges. |
| `groups` | Show groups of the current user. |

## 4. Permissions and Ownership
| Command | Description |
|---------|-------------|
| `chmod <permissions> <file>` | Change file permissions. Example: `chmod 755 file.txt`. |
| `chown <owner>:<group> <file>` | Change the ownership of a file. Example: `chown user file`. |
| `ls -l` | View file permissions in detail. |

## 5. Process Management
| Command | Description |
|---------|-------------|
| `ps` | Show currently running processes. |
| `ps aux` | Show detailed information about all processes. |
| `top` | Display real-time system stats (CPU, memory usage, processes). |
| `htop` | Interactive version of top (needs installation). |
| `kill <PID>` | Terminate a process by its Process ID (PID). |
| `killall <name>` | Terminate all processes by name. |
| `bg` | Resume a job in the background. |
| `fg` | Resume a job in the foreground. |

## 6. Networking
| Command | Description |
|---------|-------------|
| `ping <host>` | Test network connectivity to a host. |
| `ifconfig` | Display network interface information (needs installation). |
| `ip addr` | Display network interfaces and IP addresses. |
| `nslookup <domain>` | Get DNS information for a domain. |
| `curl <url>` | Fetch the contents of a URL. |
| `wget <url>` | Download files from a URL. |

## 7. Disk and Filesystem
| Command | Description |
|---------|-------------|
| `df -h` | Display disk space usage in human-readable format. |
| `du -sh <file/directory>` | Show the size of a file or directory. |
| `mount <device> <directory>` | Mount a filesystem. |
| `umount <directory>` | Unmount a filesystem. |
| `lsblk` | Display information about block devices. |
| `blkid` | Display block device attributes (UUID, type, etc.). |
| `fdisk -l` | List disk partitions. |

## 8. Compression and Archiving
| Command | Description |
|---------|-------------|
| `tar -cvf <archive>.tar <files>` | Create a tar archive. |
| `tar -xvf <archive>.tar` | Extract a tar archive. |
| `tar -czvf <archive>.tar.gz <files>` | Create a compressed tar archive. |
| `tar -xzvf <archive>.tar.gz` | Extract a compressed tar archive. |
| `gzip <file>` | Compress a file. |
| `gunzip <file>.gz` | Decompress a `.gz` file. |
| `zip <archive>.zip <files>` | Create a zip archive. |
| `unzip <archive>.zip` | Extract a zip archive. |

## 9. System Information
| Command | Description |
|---------|-------------|
| `uname -a` | Display system information (kernel, architecture, etc.). |
| `hostname` | Show the system hostname. |
| `uptime` | Show how long the system has been running. |
| `free -h` | Display memory usage in human-readable format. |
| `df -h` | Show disk space usage in human-readable format. |
| `lscpu` | Display CPU information. |
| `lsusb` | List USB devices. |
| `lspci` | List PCI devices. |

## 10. Package Management

### For Debian/Ubuntu (apt-based systems):
| Command | Description |
|---------|-------------|
| `apt update` | Update package lists. |
| `apt upgrade` | Upgrade all installed packages. |
| `apt install <package>` | Install a new package. |
| `apt remove <package>` | Remove a package. |
| `apt autoremove` | Remove unused dependencies. |
| `dpkg -i <package>.deb` | Install a `.deb` package. |

### For RHEL/CentOS/Fedora (yum-based systems):
| Command | Description |
|---------|-------------|
| `yum update` | Update all installed packages. |
| `yum install <package>` | Install a new package. |
| `yum remove <package>` | Remove a package. |
| `rpm -ivh <package>.rpm` | Install an `.rpm` package. |

## 11. Searching and Grep
| Command | Description |
|---------|-------------|
| `grep <pattern> <file>` | Search for a pattern in a file. |
| `grep -i <pattern> <file>` | Case-insensitive search. |
| `grep -r <pattern> <directory>` | Search for a pattern recursively in a directory. |
| `find <directory> -name <name>` | Search for files by name. |
