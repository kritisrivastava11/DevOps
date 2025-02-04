# **Linux For DevOps**

## **1\. Introduction to Linux**

* Linux is an open-source operating system based on Unix.  
* Key distributions (distros): Ubuntu, CentOS, Debian, Fedora, Arch Linux.  
* Linux kernel: The core of the OS managing hardware and system processes.

## **2\. Linux Architecture**

* **Kernel**: Core of the OS that interacts with hardware.  
* **Shell**: Interface that allows users to interact with the system.  
* **File System**: Organizes and manages files.  
* **User Space**: Includes applications and utilities.

  

## **3\. Basic Linux Commands**

* `pwd` – Print working directory.  
* `ls` – List directory contents.  
* `cd` – Change directory.  
* `mkdir` – Create a new directory.  
* `rmdir` – Remove an empty directory.  
* `rm -r` – Remove directory with files.  
* `touch` – Create a new empty file.  
* `cp` – Copy files and directories.  
* `mv` – Move/rename files.  
* `rm` – Remove files.  
* `cat` – View file content.  
* `less` – View file content page by page.  
* `echo` – Print text or append to files.  
* `man` – Display manual for commands.  
* `chmod` – Change file permissions.  
* `chown` – Change file owner.  
* `find` – Search for files.  
* `grep` – Search inside files.  
* `awk` – Text processing and pattern scanning tool.  
* `sed` – Stream editor for modifying text.

## **4\. User and Group Management**

* `whoami` – Display current user.  
* `who` – List logged-in users.  
* `id` – Display user ID (UID) and group ID (GID).  
* `adduser username` – Add a new user.  
* `deluser username` – Remove a user.  
* `passwd username` – Change user password.  
* `usermod -aG groupname username` – Add a user to a group.  
* `groups username` – Show groups of a user.  
* `groupadd groupname` – Create a new group.

## **5\. File Permissions**

* `ls -l` – Show file permissions.  
* Permission types: Read (r), Write (w), Execute (x).  
* Change permissions: `chmod 744 filename`  
* Change ownership: `chown user:group filename`

The first digit is for owner permissions, the second digit is for group permissions, and the third is for other users. Each permission has a numeric value assigned to it:

* r (read): 4  
* w (write): 2  
* x (execute): 1

In the permission value 744, the first digit corresponds to the user, the second digit to the group, and the third digit to others. By adding up the value of each user classification, you can find the file permissions.  
For example, a file might have read, write, and execute permissions for its owner, and only read permission for all other users. That looks like this:

* Owner: rwx \= 4+2+1 \= 7  
* Group: r-- \= 4+0+0 \= 4  
* Others: r-- \= 4+0+0 \= 4

The results produce the three-digit value 744\.

## **6\. Sudo (Superuser Privileges)**

* `sudo command` – Run command as a superuser.  
* `sudo su` – Switch to the root user.  
* `visudo` – Edit sudo privileges securely.

## **7\. Package Management**

* **Debian-based (Ubuntu, Debian)**:  
  * `apt update && apt upgrade` – Update system packages.  
  * `apt install package-name` – Install a package.  
  * `apt remove package-name` – Remove a package.  
* **RHEL-based (CentOS, Fedora)**:  
  * `yum update` / `dnf update`  
  * `yum install package-name`  
  * `yum remove package-name`

## **8\. Process Management**

* `ps` – Show running processes.  
* `top` – Display system processes in real-time.  
* `htop` – Interactive process viewer.  
* `kill PID` – Terminate a process.  
* `killall processname` – Kill all instances of a process.  
* `nice` – Run process with a priority.  
* `renice` – Change process priority.  
* `nohup command &` – Run a command in the background.  
* `jobs` – List background processes.  
* `fg` – Bring a background process to the foreground.  
* `bg` – Resume a background process.

## **9\. Networking**

* `ifconfig` / `ip a` – Show IP addresses.  
* `ping domain.com` – Test network connectivity.  
* `netstat -tulnp` – Show active connections.  
* `curl` / `wget` – Fetch data from URLs.  
* `scp` – Secure copy files between servers.  
* `rsync` – Synchronize files between servers.

### **Connecting from One VM to Another**

* **Using SSH:**  
  ssh user@remote-vm-ip  
* **Using SCP to transfer files:**  
  scp filename user@remote-vm-ip:/destination/path  
* **SSH Key-based Authentication:**  
  * **Generate SSH Key on First Server:**  
    ssh-keygen \-t rsa \-b 4096  
  * Copy the public key to the second server:  
    ssh-copy-id user@remote-vm-ip  
  * Alternatively, manually copy `~/.ssh/id_rsa.pub` to `~/.ssh/authorized_keys` on the second server.  
  * Ensure proper permissions:  
    chmod 600 \~/.ssh/authorized\_keys  
  * **SSH into the second server using the private key:**  
    ssh \-i \~/.ssh/id\_rsa user@remote-vm-ip

## **10\. Shell Scripting Basics**

* **What is Shell Scripting?**  
  * Shell scripting is writing a series of commands in a file to automate tasks.

\#\!/bin/bash  
echo "Hello, World\!"

* Save as `script.sh`, then run:  
  chmod \+x script.sh  
* ./script.sh  
* Variables: `name="Kriti"`  
* Conditional statements: `if, else, elif`  
* Loops: `for, while`  
* Functions: `function myFunc() { commands }`

## **11\. Hosting a Web Page Using Nginx**

**Install Nginx:**  
sudo apt update

* sudo apt install nginx

**Start and Enable Nginx:**  
sudo systemctl start nginx

* sudo systemctl enable nginx  
* **Place Web Files:**  
  * Default root directory: `/var/www/html/`  
  * Place your `index.html` file there.  
* **Restart Nginx:**  
  sudo systemctl restart nginx  
* Access via browser using `http://your-server-ip`

## **12\. Linux Volumes (Storage Management)**

* `lsblk` – List block devices.  
* `fdisk -l` – Show disk partitions.  
* `mount /dev/sdX /mnt` – Mount a disk.  
* `umount /mnt` – Unmount a disk.  
* `df -h` – Show disk space usage.  
* `du -sh directory` – Show directory size.

## **13\. System Monitoring & Logs**

* `uptime` – Show system uptime.  
* `free -m` – Display memory usage.  
* `vmstat` – Show system performance stats.  
* `dmesg` – Kernel logs.  
* `journalctl -xe` – View system logs.  
* `tail -f /var/log/syslog` – View live logs.

## **14\. Advanced Topics**

### **Cron Jobs (Task Scheduling)**

* `crontab -e` – Edit cron jobs.  
* Example: Run a script every day at 3 AM:  
  0 3 \* \* \* /path/to/script.sh

### **Firewall Management**

* `ufw status` – Check firewall status.  
* `ufw allow 22/tcp` – Allow SSH port.  
* `ufw enable` – Enable firewall.

### **Docker & Containers**

* `docker ps` – List running containers.  
* `docker images` – Show Docker images.  
* `docker run -d -p 8080:80 nginx` – Run Nginx container.

