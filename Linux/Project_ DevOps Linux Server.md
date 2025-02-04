## **🚀 Project: DevOps Linux Server Monitoring & Automation**

Imagine you're managing a Linux-based production server and need to ensure that users, logs, and processes are well-managed. You will perform real-world tasks such as log analysis, volume management, and automation to enhance your DevOps skills.

---

## **📌 Tasks**

### **1️⃣ User & Group Management**

* Learn about Linux users, groups, and permissions (`/etc/passwd`, `/etc/group`).  
* Task:  
  * Create a user `devops_user` and add them to a group `devops_team`.  
  * Set a password and grant sudo access.  
  * Restrict SSH login for certain users in `/etc/ssh/sshd_config`.

---

### **2️⃣ File & Directory Permissions**

* Task:  
  * Create `/devops_workspace` and a file `project_notes.txt`.  
  * Set permissions:  
    * Owner can edit, group can read, others have no access.  
  * Use `ls -l` to verify permissions.

---

### **3️⃣ Log File Analysis with AWK, Grep & Sed**

Logs are crucial in DevOps\! You’ll analyze logs using the Linux\_2k.log file from LogHub ([GitHub Repo](https://github.com/logpai/loghub/blob/master/Linux/Linux_2k.log)).

* Task:  
  * Download the log file from the repository.  
  * Extract insights using commands:  
    * Use `grep` to find all occurrences of the word "error".  
    * Use `awk` to extract timestamps and log levels.  
    * Use `sed` to replace all IP addresses with \[REDACTED\] for security.  
  * Bonus: Find the most frequent log entry using `awk` or `sort | uniq -c | sort -nr | head -10`.

---

### **4️⃣ Volume Management & Disk Usage**

* Task:  
  * Create a directory `/mnt/devops_data`.  
  * Mount a new volume (or loop device for local practice).  
  * Verify using `df -h` and `mount | grep devops_data`.

---

### **5️⃣ Process Management & Monitoring**

* Task:  
  * Start a background process (`ping google.com > ping_test.log &`).  
  * Use `ps`, `top`, and `htop` to monitor it.  
  * Kill the process and verify it's gone.

---

### **6️⃣ Automate Backups with Shell Scripting**

* Task:  
  * Write a shell script to back up `/devops_workspace` as `backup_$(date +%F).tar.gz`.  
  * Save it in `/backups` and schedule it using `cron`.  
  * Make the script display a success message in green text using `echo -e`.

---

## **🎯 Bonus Tasks (Optional 🚀)**

1. Find the top 5 most common log messages in `Linux_2k.log` using `awk` and `sort`.  
2. Use `find` to list all files modified in the last 7 days.  
3. Write a script that extracts and displays only ERROR and WARNING logs from `Linux_2k.log`.

   **Solution**

### **1️⃣ User & Group Management**

`# Create group`  
`sudo groupadd devops_team`

`# Create user and add to group`  
`sudo useradd -m -G devops_team -s /bin/bash devops_user`

`# Set password for user`  
`echo "devops_user:password" | sudo chpasswd`

`# Grant sudo access`  
`sudo usermod -aG sudo devops_user`

`# Restrict SSH login for certain users`  
`echo "DenyUsers restricted_user" | sudo tee -a /etc/ssh/sshd_config`  
`sudo systemctl restart sshd`

### **2️⃣ File & Directory Permissions**

`# Create directory and file`  
`sudo mkdir -p /devops_workspace`  
`sudo touch /devops_workspace/project_notes.txt`

`# Set permissions: owner can edit, group can read, others have no access`  
`sudo chown devops_user:devops_team /devops_workspace/project_notes.txt`  
`sudo chmod 640 /devops_workspace/project_notes.txt`

`# Verify permissions`  
`ls -l /devops_workspace`

### **3️⃣ Log File Analysis with AWK, Grep & Sed**

`# Download the log file`  
`wget -O Linux_2k.log https://github.com/some-repo/Linux_2k.log  # Replace with actual URL`

`# Find occurrences of the word "error"`  
`grep "error" Linux_2k.log`

`# Extract timestamps and log levels`  
`awk '{print $1, $2, $3, $5}' Linux_2k.log`

`# Replace all IP addresses with [REDACTED]`  
`sed -E 's/[0-9]+\.[0-9]+\.[0-9]+\.[0-9]+/[REDACTED]/g' Linux_2k.log | head -10`

`# Find the most frequent log entry`  
`awk '{print $5}' Linux_2k.log | sort | uniq -c | sort -nr | head -10`

### **4️⃣ Volume Management & Disk Usage**

`# Create directory`  
`sudo mkdir -p /mnt/devops_data`

`# Mount a new volume (adjust /dev/sdb1 as per your setup)`  
`sudo mount /dev/sdb1 /mnt/devops_data`

`# Verify disk usage and mount status`  
`df -h | grep devops_data`  
`mount | grep devops_data`

### **5️⃣ Process Management & Monitoring**

`# Start background process`  
`ping google.com > ping_test.log &`

`# Monitor processes`  
`ps aux | grep ping`  
`top -b -n1 | head -20`  
`htop  # (If installed)`

`# Kill the process`  
`pkill -f "ping google.com"`

`# Verify it's gone`  
`ps aux | grep ping`

### **6️⃣ Automate Backups with Shell Scripting**

`# Create backup`  
`tar -czf /backups/backup_$(date +%F).tar.gz /devops_workspace`

`# Schedule backup via cron (edit crontab)`  
`echo "0 2 * * * tar -czf /backups/backup_$(date +%F).tar.gz /devops_workspace && echo -e '\e[32mBackup successful!\e[0m'" | sudo tee -a /etc/crontab`

### **🎯 Bonus Tasks**

`# Find the top 5 most common log messages`  
`awk '{print $5}' Linux_2k.log | sort | uniq -c | sort -nr | head -5`

`# List all files modified in the last 7 days`  
`find / -type f -mtime -7 2>/dev/null`

`# Extract only ERROR and WARNING logs`  
`grep -E "(ERROR|WARNING)" Linux_2k.log`  
