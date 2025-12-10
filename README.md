# 🗄️ **mynas** - Linux NAS Management Tool

**Repository:** [https://github.com/KYGnus/mynas.git](https://github.com/KYGnus/mynas.git)  
**Developer:** KYGnus  
**Main Script:** `mynas.sh`  
**Configuration Script:** `configure`  

## 📖 Overview

**mynas** is a comprehensive command-line tool that converts Linux systems into fully-featured NAS (Network Attached Storage) servers with enterprise-grade management capabilities. The system includes two main components:

1. **`mynas.sh`** - Main management tool with modular commands
2. **`configure`** - Installation script to set up the NAS environment

## 🚀 Quick Installation

### Method 1: One-Command Installation
```bash
# Clone the repository
git clone https://github.com/KYGnus/mynas.git
cd mynas

# Make scripts executable
chmod +x configure mynas.sh

# Run the configuration script
sudo ./configure --users admin,user1,user2
```

### Method 2: Manual Installation
```bash
# Clone repository
git clone https://github.com/KYGnus/mynas.git
cd mynas

# Copy main script
sudo cp mynas.sh /usr/local/bin/mynas
chmod +x /usr/local/bin/mynas

# Run configuration
sudo ./configure
```

## 📋 Complete Command Reference

### 🆘 **Help & Information**
```bash
# Show main help
mynas --help

# Show module-specific help
mynas --help --user
mynas --help --group
mynas --help --storage

# Show version
mynas --version

# Enable verbose output
mynas --verbose --storage --list
```

### 👤 **User Management**
```bash
# Add a new user
mynas --user --add john
mynas --user --add mary /bin/bash

# Remove a user
mynas --user --remove john
mynas --user --remove mary yes  # Keep home directory

# List all users
mynas --user --list

# Change password
mynas --user --passwd john

# Add user to group
mynas --user --add-to-group john developers

# Remove user from group
mynas --user --remove-from-group john developers

# Lock/unlock account
mynas --user --lock john
mynas --user --unlock john

# Show user information
mynas --user --info john

# List user groups
mynas --user --list-groups john
```

### 👥 **Group Management**
```bash
# Create a new group
mynas --group --create developers
mynas --group --create managers
mynas --group --create nasusers

# Delete a group
mynas --group --delete developers

# Add user to group
mynas --group --adduser developers john
mynas --group --adduser nasusers mary

# Remove user from group
mynas --group --removeuser developers john

# List all groups
mynas --group --list

# List group members
mynas --group --list developers

# Set group ownership
mynas --group --setowner developers admin
```

### 🔐 **Access Policy Management**
```bash
# Create access policy
mynas --policy --create dev_access developers /mnt/nas/projects rw yes
mynas --policy --create mgr_access managers /mnt/nas/confidential r no
mynas --policy --create read_only guests /mnt/nas/public r yes

# Delete policy
mynas --policy --delete dev_access

# Apply specific policy
mynas --policy --apply dev_access

# Apply all policies
mynas --policy --applyall

# List all policies
mynas --policy --list

# List specific policy details
mynas --policy --list dev_access

# Test user access
mynas --policy --test john /mnt/nas/projects
mynas --policy --test mary /mnt/nas/confidential
```

### 💾 **Storage Management**
```bash
# List storage devices
mynas --storage --list

# Format device
mynas --storage --format /dev/sdb1 ext4
mynas --storage --format /dev/sdc1 xfs

# Mount device
mynas --storage --mount /dev/sdb1 /mnt/data

# Unmount device
mynas --storage --umount /mnt/data

# Show device information
mynas --storage --info /dev/sdb
mynas --storage --info /dev/nvme0n1
```

### 🛡️ **RAID Management**
```bash
# Create RAID array
mynas --raid --create 0 /dev/sdb /dev/sdc md0          # RAID 0
mynas --raid --create 1 /dev/sdb /dev/sdc md1          # RAID 1
mynas --raid --create 5 /dev/sdb /dev/sdc /dev/sdd md5 # RAID 5
mynas --raid --create 10 /dev/sdb /dev/sdc /dev/sdd /dev/sde md10 # RAID 10

# Add device to RAID
mynas --raid --add md0 /dev/sde

# Remove device from RAID
mynas --raid --remove md0 /dev/sde

# Stop RAID array
mynas --raid --stop md0

# Show RAID status
mynas --raid --status

# Save RAID configuration
mynas --raid --save
```

### 🔧 **LVM Management**
```bash
# Create physical volume
mynas --lvm --create-pv /dev/sdb
mynas --lvm --create-pv /dev/sdc

# Create volume group
mynas --lvm --create-vg vg_data /dev/sdb /dev/sdc

# Create logical volume
mynas --lvm --create-lv vg_data lv_storage 100G
mynas --lvm --create-lv vg_data lv_backup 50G

# Extend logical volume
mynas --lvm --extend-lv /dev/vg_data/lv_storage +50G

# Reduce logical volume
mynas --lvm --reduce-lv /dev/vg_data/lv_storage 80G

# List physical volumes
mynas --lvm --list-pv

# List volume groups
mynas --lvm --list-vg

# List logical volumes
mynas --lvm --list-lv

# Remove logical volume
mynas --lvm --remove-lv /dev/vg_data/lv_backup

# Remove volume group
mynas --lvm --remove-vg vg_data

# Remove physical volume
mynas --lvm --remove-pv /dev/sdb
```

### 📁 **Advanced Filesystem Management**
```bash
# Resize filesystem
mynas --fs-advanced --resize /dev/vg_data/lv_storage
mynas --fs-advanced --resize /dev/sdb1 50G

# Check filesystem
mynas --fs-advanced --check /dev/sdb1
mynas --fs-advanced --check /dev/sdb1 ext4
mynas --fs-advanced --check /dev/sdb1 xfs

# Set filesystem label
mynas --fs-advanced --label /dev/sdb1 "NAS_Storage"
mynas --fs-advanced --label /dev/vg_data/lv_storage "Data_Volume"

# Tune filesystem parameters
mynas --fs-advanced --tune /dev/sdb1 reserved 1
mynas --fs-advanced --tune /dev/sdb1 mounts 30
mynas --fs-advanced --tune /dev/sdb1 interval 2w

# Defragment filesystem
mynas --fs-advanced --defrag /mnt/nas

# Swap management
mynas --fs-advanced --swap /dev/sdb2 create
mynas --fs-advanced --swap /dev/sdb2 enable
mynas --fs-advanced --swap /dev/sdb2 disable
mynas --fs-advanced --swap /dev/sdb2 remove
mynas --fs-advanced --swap /dev/sdb2 status
```

### 📤 **Share Management**
```bash
# Create Samba share
mynas --samba --install
mynas --samba --add-share Data /mnt/nas/data nasusers yes

# Create NFS share
mynas --nfs --install
mynas --nfs --add-share /mnt/nas/data 192.168.1.0/24

# Configure SSHFS
mynas --sshfs --install
mynas --sshfs --mount user@server /remote/path /local/path
```

### 🔒 **Permission Management**
```bash
# Set permissions
mynas --permission --set /mnt/nas/data root nasusers 2770
mynas --permission --set /mnt/nas/projects john developers 2775

# Fix permissions recursively
mynas --permission --fix /mnt/nas

# Check permissions
mynas --permission --check /mnt/nas/data
mynas --permission --check /mnt/nas/projects john

# Set up permission inheritance
mynas --permission --inherit /mnt/nas/data
```

### 🛡️ **Security Management**
```bash
# Firewall management
mynas --firewall --add-port 445/tcp
mynas --firewall --add-service samba
mynas --firewall --add-source 192.168.1.0/24
mynas --firewall --list

# Fail2ban management
mynas --fail2ban --install
mynas --fail2ban --enable-jail sshd
mynas --fail2ban --enable-jail samba
mynas --fail2ban --status

# Antivirus management
mynas --av --clamav /mnt/nas
mynas --av --maldet /mnt/nas
mynas --av --rkhunter
mynas --av --chkrootkit
mynas --av --update-databases
mynas --av --clamav-schedule /mnt/nas
mynas --av --maldet-monitor /mnt/nas
```

### 📈 **Monitoring Management**
```bash
# System monitoring
mynas --monitor --iostat 2 10
mynas --monitor --disk-health

# NetData management
mynas --monitor --netdata start
mynas --monitor --netdata stop
mynas --monitor --netdata restart
mynas --monitor --netdata status
```

### 💾 **Backup Management**
```bash
# Create backups
mynas --backup --tar /mnt/nas /mnt/backup/nas_backup.tar.gz
mynas --backup --zip /mnt/nas /mnt/backup/nas_backup.zip
mynas --backup --dd /dev/vg_data/lv_storage /mnt/backup/disk_image.img
```

### 🔧 **System Management**
```bash
# Update system
mynas --system --update

# Service management
mynas --service --start smbd
mynas --service --stop smbd
mynas --service --restart smbd
mynas --service --enable smbd
mynas --service --disable smbd
mynas --service --status smbd
mynas --service --mask smbd
mynas --service --unmask smbd

# Network management
mynas --network --list-interfaces
mynas --network --set-ip eth0 192.168.1.100 24
mynas --network --set-gateway 192.168.1.1
mynas --network --set-dns 8.8.8.8
mynas --network --test
```

## 🎯 **Configure Script Examples**

### Basic Setup Examples

**Example 1: Home NAS Setup**
```bash
sudo ./configure --users family,guests,media
```

**Example 2: Small Business NAS**
```bash
sudo ./configure \
    --users admin,finance,sales,it \
    --nas-mount /company \
    --backup-dir /backup/company \
    --nfs-cidr 10.0.0.0/16
```

**Example 3: Development Team NAS**
```bash
sudo ./configure \
    --users dev1,dev2,dev3,qa,prod \
    --nas-mount /projects \
    --nfs-cidr 172.16.0.0/12 \
    --smb-share /projects/smb \
    --nfs-share /projects/nfs
```

**Example 4: Media Server**
```bash
sudo ./configure \
    --users media,family,guests \
    --nas-mount /media \
    --backup-dir /backup/media
```

**Example 5: Complete Enterprise Setup**
```bash
sudo ./configure \
    --users admin,john,mary,finance,hr,it \
    --nas-mount /enterprise \
    --backup-dir /backup/enterprise \
    --nfs-cidr 192.168.100.0/24 \
    --smb-share /enterprise/shares \
    --nfs-share /enterprise/exports
```

### Advanced Configuration Examples

**Example 6: Multi-Environment Setup**
```bash
# Development environment
sudo ./configure --users dev1,dev2 --nas-mount /dev --nfs-cidr 192.168.1.0/24

# Production environment
sudo ./configure --users prod1,prod2 --nas-mount /prod --nfs-cidr 10.0.0.0/16

# Backup server
sudo ./configure --users backup --nas-mount /backup --backup-dir /backup/main
```

**Example 7: Departmental NAS**
```bash
# Finance department
sudo ./configure --users finance1,finance2 --nas-mount /finance

# HR department
sudo ./configure --users hr1,hr2 --nas-mount /hr

# IT department
sudo ./configure --users it1,it2,admin --nas-mount /it
```

## 🏗️ **Complete Workflow Example**

### Scenario: Setting up a Development Team NAS

```bash
# Step 1: Configure the system
sudo ./configure --users dev1,dev2,dev3,qa --nas-mount /devteam

# Step 2: Create groups
mynas --group --create developers
mynas --group --create testers
mynas --group --create managers

# Step 3: Add users to groups
mynas --group --adduser developers dev1
mynas --group --adduser developers dev2
mynas --group --adduser developers dev3
mynas --group --adduser testers qa
mynas --group --adduser managers admin

# Step 4: Create storage structure
mynas --storage --format /dev/sdb1 ext4
mynas --storage --mount /dev/sdb1 /devteam/projects

# Step 5: Create RAID for backup
mynas --raid --create 1 /dev/sdc /dev/sdd md0
mynas --storage --format /dev/md0 ext4
mynas --storage --mount /dev/md0 /devteam/backup

# Step 6: Set up access policies
mynas --policy --create dev_projects developers /devteam/projects rwx yes
mynas --policy --create test_access testers /devteam/projects r yes
mynas --policy --create mgr_access managers /devteam/projects rw yes

# Step 7: Apply policies
mynas --policy --applyall

# Step 8: Set up Samba
mynas --samba --install
mynas --samba --add-share Projects /devteam/projects developers yes

# Step 9: Set up NFS
mynas --nfs --install
mynas --nfs --add-share /devteam/projects 192.168.1.0/24

# Step 10: Configure security
mynas --firewall --add-service samba
mynas --firewall --add-service nfs
mynas --fail2ban --install

# Step 11: Set up monitoring
mynas --monitor --netdata start

# Step 12: Schedule backups
mynas --backup --tar /devteam/projects /devteam/backup/projects_$(date +%Y%m%d).tar.gz

# Step 13: Verify setup
mynas --storage --list
mynas --raid --status
mynas --policy --test dev1 /devteam/projects
```

## 🗂️ **Directory Structure After Configuration**

```
/
├── /mnt/nas/                    # Main NAS mount
│   ├── data/                   # Data storage
│   ├── shares/                 # Shared files
│   ├── groups/                 # Group directories
│   ├── projects/               # Project files
│   └── backup/                 # Local backups
├── /etc/mynas/                 # Configuration
│   ├── groups.conf            # Group definitions
│   ├── policies.conf          # Access policies
│   ├── shares.conf           # Share definitions
│   └── apply_policies.sh     # Policy script
├── /var/log/mynas/            # Logs
│   ├── access.log            # Access logs
│   ├── error.log             # Error logs
│   └── audit.log             # Audit logs
└── /usr/local/bin/            # Tools
    └── mynas                 # Main executable
```

## 📊 **Post-Installation Checklist**

### 🔐 **Immediate Security Actions**
1. **Change default passwords:**
   ```bash
   passwd username
   smbpasswd username
   ```

2. **Review firewall rules:**
   ```bash
   firewall-cmd --list-all
   ```

3. **Check service security:**
   ```bash
   systemctl status fail2ban
   tail -f /var/log/fail2ban.log
   ```

### 🛠️ **Configuration Steps**
4. **Configure shares:**
   - Edit `/etc/mynas/shares.conf`
   - Apply changes: `/etc/mynas/apply_policies.sh`

5. **Set up monitoring:**
   - Access NetData: `http://<server-ip>:19999`

6. **Schedule backups:**
   - Review `/etc/cron.weekly/nas-backup`

### 🔍 **Verification Tests**
7. **Test Samba access:**
   ```bash
   smbclient -L localhost -U username
   ```

8. **Test NFS access:**
   ```bash
   showmount -e localhost
   ```

9. **Test monitoring:**
   ```bash
   nas-monitor
   ```

## 🔄 **Maintenance Commands**

```bash
# Weekly maintenance
mynas --system --update
mynas --av --update-databases
mynas --policy --applyall
mynas --backup --tar /mnt/nas /mnt/backup/weekly_backup.tar.gz

# Monthly maintenance
mynas --fs-advanced --check /mnt/nas
mynas --raid --status
```

## 📝 **License & Attribution**

**Project:** mynas  
**Repository:** [https://github.com/KYGnus/mynas.git](https://github.com/KYGnus/mynas.git)  
**Developer:** KYGnus  
**Main Script:** `mynas`  
**Configuration Script:** `configure`

## 🤝 **Contributing**

1. Fork the repository
2. Create a feature branch
3. Commit your changes
4. Push to the branch
5. Create a Pull Request



## 📚 **Documentation**

- **Online:** [GitHub Repository](https://github.com/KYGnus/mynas)
- **Local:** Check `/etc/mynas/README` after installation
- **Man Pages:** `man mynas` (after installation)

---

**Note:** Always test commands in a safe environment first. The `configure` script is idempotent and can be safely re-run if needed.

For real-time help, use: `mynas --help --[module]`