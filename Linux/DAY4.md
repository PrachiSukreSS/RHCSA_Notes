//File Hierarchy sturcture 
Here's a comprehensive `README.md` file for Linux File System Hierarchy:

```markdown
# Linux File System Hierarchy (FHS)

A comprehensive guide to the Linux File System Hierarchy Standard (FHS) with commands, descriptions, and directory structures for RHCSA exam preparation.

## Table of Contents

- [Introduction to FHS](#introduction-to-fhs)
- [Root Directory Structure](#root-directory-structure)
- [Essential Directories Explained](#essential-directories-explained)
  - [System Binaries](#system-binaries)
  - [Configuration Files](#configuration-files)
  - [User Data](#user-data)
  - [Variable Data](#variable-data)
  - [Device Files](#device-files)
  - [Process Information](#process-information)
- [File System Management Commands](#file-system-management-commands)
- [Disk Management](#disk-management)
- [Mounting File Systems](#mounting-file-systems)
- [Important Commands Summary](#important-commands-summary)
- [Quick Reference Tips](#quick-reference-tips)
- [Practice Checklist](#practice-checklist)

---

## Introduction to FHS

The **Filesystem Hierarchy Standard (FHS)** defines the directory structure and directory contents in Linux distributions. It provides a consistent layout that allows users and software to predict where files are located.

**🔑 Key Principles:**
- **Shareable vs. Unshareable**: Data that can be shared vs. host-specific data
- **Static vs. Variable**: Files that don't change vs. files that change frequently

| Type | Shareable | Unshareable |
|------|-----------|-------------|
| **Static** | `/usr`, `/opt` | `/etc`, `/boot` |
| **Variable** | `/var/mail` | `/var/run`, `/var/lock` |

---

## Root Directory Structure

```
/                   # Root directory - top of file system hierarchy
├── bin/            # Essential user command binaries
├── boot/           # Boot loader files (kernel, initramfs)
├── dev/            # Device files
├── etc/            # Host-specific system configuration
├── home/           # User home directories
├── lib/            # Essential shared libraries
├── lib64/          # 64-bit shared libraries
├── media/          # Mount point for removable media
├── mnt/            # Mount point for temporary file systems
├── opt/            # Optional application software packages
├── proc/           # Virtual file system for process information
├── root/           # Home directory for root user
├── run/            # Run-time variable data
├── sbin/           # System administration binaries
├── srv/            # Data for services provided by system
├── sys/            # Virtual file system for system information
├── tmp/            # Temporary files
├── usr/            # Secondary hierarchy (user programs)
│   ├── bin/        # User command binaries
│   ├── lib/        # Libraries for user binaries
│   ├── local/      # Local hierarchy
│   ├── sbin/       # System binaries
│   └── share/      # Architecture-independent data
└── var/            # Variable data (logs, spool files)
    ├── cache/      # Application cache data
    ├── lib/        # Variable state information
    ├── log/        # Log files
    ├── mail/       # User mailbox files
    ├── spool/      # Spool directories
    └── tmp/        # Temporary files preserved between reboots
```

---

## Essential Directories Explained

### System Binaries

| Directory | Purpose | Key Commands |
|-----------|---------|--------------|
| **`/bin`** | Essential user command binaries required for system recovery | `ls`, `cp`, `mv`, `rm`, `bash` |
| **`/sbin`** | Essential system binaries for system administration | `fdisk`, `ifconfig`, `mount`, `reboot` |
| **`/usr/bin`** | Most user commands | `vim`, `gcc`, `python` |
| **`/usr/sbin`** | Non-essential system binaries | `httpd`, `sshd` |
| **`/usr/local/bin`** | Locally installed user binaries | Custom scripts, manually installed software |
| **`/usr/local/sbin`** | Locally installed system binaries | Locally installed daemons |

**💡 Tips:**
- `/bin` and `/sbin` are essential for system boot and recovery
- `/usr/bin` and `/usr/sbin` can be mounted separately
- `/usr/local` is for software installed manually (not via package manager)

### Configuration Files

| Directory | Purpose | Examples |
|-----------|---------|----------|
| **`/etc`** | System-wide configuration files | `passwd`, `fstab`, `hostname`, `ssh/` |
| **`/etc/sysconfig`** | System configuration files (RHEL-specific) | Network, SELinux, firewall |
| **`/etc/default`** | Default configuration for packages | `useradd`, `grub` |
| **`/etc/init.d`** | System V init scripts | Service startup scripts |
| **`/etc/systemd`** | Systemd configuration | Unit files, system configuration |

**Common Configuration Files:**
```bash
/etc/passwd          # User account information
/etc/shadow          # Encrypted passwords
/etc/group           # Group information
/etc/fstab           # File system mount configuration
/etc/hostname        # System hostname
/etc/hosts           # Local hostname resolution
/etc/resolv.conf     # DNS resolver configuration
/etc/ssh/sshd_config # SSH server configuration
/etc/sudoers         # Sudo privileges
```

### User Data

| Directory | Purpose | Usage |
|-----------|---------|-------|
| **`/home`** | User home directories | `/home/username/` |
| **`/root`** | Root user's home directory | Only accessible by root |
| **`/home/username`** | Individual user's personal files | Documents, downloads, configurations |

**Home Directory Structure:**
```bash
/home/username/
├── .bashrc          # User's bash configuration
├── .bash_profile    # User's login profile
├── .ssh/            # SSH keys and configuration
├── Documents/       # User documents
├── Downloads/       # Downloaded files
├── Desktop/         # Desktop files
└── .config/         # Application configurations
```

### Variable Data

| Directory | Purpose | Contents |
|-----------|---------|----------|
| **`/var/log`** | System log files | `messages`, `secure`, `cron`, `audit/` |
| **`/var/cache`** | Application cache | Package manager cache, application data |
| **`/var/lib`** | Variable state information | Databases, package manager state |
| **`/var/spool`** | Spool directories | Mail queues, print queues, cron jobs |
| **`/var/tmp`** | Persistent temporary files | Files preserved between reboots |
| **`/var/run`** | Run-time variable data | PID files, system state (now `/run`) |

**Important Log Files:**
```bash
/var/log/messages    # General system messages
/var/log/secure      # Security and authentication logs
/var/log/maillog     # Mail server logs
/var/log/cron        # Cron job logs
/var/log/dmesg       # Kernel ring buffer
/var/log/boot.log    # System boot logs
```

### Device Files

| Directory | Purpose | Examples |
|-----------|---------|----------|
| **`/dev`** | Device files | Hard disks, terminals, random number generator |

**Device Types:**
```bash
/dev/sda            # First SCSI/SATA disk
/dev/sda1           # First partition on first disk
/dev/nvme0n1        # First NVMe SSD
/dev/nvme0n1p1      # First partition on NVMe SSD
/dev/null           # Null device (data sink)
/dev/zero           # Zero device (provides zeros)
/dev/random         # Random number generator (blocking)
/dev/urandom        # Random number generator (non-blocking)
/dev/tty1           # First virtual terminal
```

### Process Information

| Directory | Purpose | Contents |
|-----------|---------|----------|
| **`/proc`** | Virtual file system for process and kernel information | Running processes, kernel parameters |
| **`/sys`** | Virtual file system for device and driver information | Kernel objects, device attributes |

**Important /proc Entries:**
```bash
/proc/cpuinfo       # CPU information
/proc/meminfo       # Memory information
/proc/partitions    # Disk partitions
/proc/version       # Kernel version
/proc/uptime        # System uptime
/proc/PID/          # Process-specific directory
/proc/self/         # Current process directory
```

---

## File System Management Commands

### File System Information

```bash
# Display disk usage
df -h               # Human-readable disk usage
df -T               # Show file system type
df -i               # Show inode usage

# Display directory size
du -sh /path        # Size of directory
du -h --max-depth=1 # Summary of first level directories

# Display file system information
lsblk               # List block devices
blkid               # Show block device attributes
fdisk -l            # List disk partitions
parted -l           # List partitions with parted
```

### File System Types

| File System | Description | Use Case |
|-------------|-------------|----------|
| **ext4** | Fourth extended file system | Default for RHEL/CentOS |
| **xfs** | High-performance 64-bit journaling | Default for RHEL 7+ |
| **btrfs** | B-tree file system | Advanced features, snapshots |
| **swap** | Swap space | Virtual memory |
| **vfat** | FAT32 | USB drives, compatibility |
| **ntfs** | NTFS | Windows compatibility |

### Creating File Systems

```bash
# Create ext4 file system
mkfs.ext4 /dev/sdb1

# Create xfs file system
mkfs.xfs /dev/sdb1

# Create swap space
mkswap /dev/sdb1

# Create file system with label
mkfs.ext4 -L data /dev/sdb1

# Create file system with custom block size
mkfs.ext4 -b 4096 /dev/sdb1
```

---

## Disk Management

### Partition Management

```bash
# Using fdisk (MBR)
fdisk /dev/sdb       # Interactive partition management
fdisk -l /dev/sdb    # List partitions

# Using parted (GPT/MBR)
parted /dev/sdb      # Interactive partition management
parted /dev/sdb print # Print partition table

# Using gdisk (GPT)
gdisk /dev/sdb       # GPT partition management
```

### Partition Creation Steps
```bash
# 1. Create partition
fdisk /dev/sdb
> n    # New partition
> p    # Primary partition
> 1    # Partition number
> +5G  # Size
> w    # Write changes

# 2. Create file system
mkfs.ext4 /dev/sdb1

# 3. Create mount point
mkdir /mnt/data

# 4. Mount file system
mount /dev/sdb1 /mnt/data

# 5. Verify mount
df -h /mnt/data
```

---

## Mounting File Systems

### Mount Commands

```bash
# Mount file system
mount /dev/sdb1 /mnt/data

# Mount with options
mount -o rw,noatime /dev/sdb1 /mnt/data

# Mount read-only
mount -o ro /dev/sdb1 /mnt/data

# Mount all file systems from /etc/fstab
mount -a

# Unmount file system
umount /mnt/data
umount /dev/sdb1

# Display mounted file systems
mount
findmnt
```

### /etc/fstab File Structure

```
# Device    Mount Point   FS Type   Options         Dump   Pass
/dev/sdb1   /mnt/data     ext4      defaults        0      0
UUID=xxx    /mnt/data     ext4      defaults        0      0
```

**Fstab Fields:**
1. **Device**: Device file or UUID (`UUID=xxx` recommended)
2. **Mount Point**: Directory where file system is mounted
3. **File System Type**: ext4, xfs, swap, etc.
4. **Options**: mount options (defaults, noatime, ro, etc.)
5. **Dump**: Backup flag (0 = no backup)
6. **Pass**: fsck order (0 = no check, 1 = root, 2 = others)

**Mount Options:**
```bash
defaults        # rw, suid, dev, exec, auto, nouser, async
ro             # Read-only
rw             # Read-write
noexec         # Prevent execution of binaries
nosuid         # Ignore suid/sgid bits
noatime        # Don't update access times
```

### Persistent Mounting
```bash
# Get UUID for persistent mounting
blkid /dev/sdb1

# Edit fstab
vi /etc/fstab
UUID=xxx /mnt/data ext4 defaults 0 0

# Test fstab entries
mount -a
```

---

## Important Commands Summary

### File System Commands

| Command | Purpose | Examples |
|---------|---------|----------|
| `df` | Report file system disk space usage | `df -h`, `df -T` |
| `du` | Estimate file space usage | `du -sh *`, `du -h --max-depth=1` |
| `lsblk` | List block devices | `lsblk`, `lsblk -f` |
| `blkid` | Show block device attributes | `blkid`, `blkid /dev/sda1` |
| `fdisk` | Partition table manipulator | `fdisk -l`, `fdisk /dev/sdb` |
| `parted` | Partition manipulation program | `parted -l`, `parted /dev/sdb` |
| `mkfs` | Build a Linux file system | `mkfs.ext4 /dev/sdb1` |
| `mount` | Mount a file system | `mount /dev/sdb1 /mnt` |
| `umount` | Unmount file systems | `umount /mnt` |
| `fsck` | Check and repair file system | `fsck /dev/sdb1` |
| `tune2fs` | Adjust file system parameters | `tune2fs -l /dev/sdb1` |
| `xfs_info` | Show XFS file system information | `xfs_info /dev/sdb1` |

### System Information Commands

| Command | Purpose | Examples |
|---------|---------|----------|
| `uname` | Print system information | `uname -a`, `uname -r` |
| `hostname` | Show or set system hostname | `hostname`, `hostnamectl` |
| `free` | Display memory usage | `free -h`, `free -m` |
| `top` | Display Linux processes | `top`, `htop` |
| `ps` | Report process status | `ps aux`, `ps -ef` |
| `lscpu` | Display CPU information | `lscpu` |
| `lsmem` | Display memory information | `lsmem` |

---

## Quick Reference Tips

### 🎯 Best Practices

1. **Always unmount before removing devices:**
   ```bash
   umount /mnt/usb
   ```

2. **Use UUID for persistent mounting:**
   ```bash
   blkid /dev/sdb1
   UUID=xxx /mnt/data ext4 defaults 0 0
   ```

3. **Check file system before mounting:**
   ```bash
   fsck -n /dev/sdb1
   ```

4. **Verify disk space before installations:**
   ```bash
   df -h /usr
   ```

5. **Monitor log files in real-time:**
   ```bash
   tail -f /var/log/messages
   ```

### 🔍 Troubleshooting Commands

```bash
# Check disk usage
df -h
du -sh /var/log

# Find large files
find / -type f -size +100M -exec ls -lh {} \;

# Check file system errors
dmesg | grep -i error
journalctl -xe

# Check mount issues
mount -a -v
findmnt

# Check disk health
smartctl -a /dev/sda
```

### 📝 Common FHS Interview Questions

1. **What is the difference between `/bin` and `/usr/bin`?**
   - `/bin` contains essential binaries for system boot/recovery
   - `/usr/bin` contains non-essential user binaries

2. **What is the purpose of `/proc` file system?**
   - Virtual file system providing process and kernel information
   - Contains runtime system information

3. **Explain the difference between `/tmp` and `/var/tmp`**
   - `/tmp` is cleared on reboot
   - `/var/tmp` preserves files between reboots

4. **What is the purpose of `/usr/local`?**
   - For locally installed software not managed by package manager
   - Hierarchy for software installed manually

5. **What are the fields in `/etc/fstab`?**
   - Device, mount point, file system type, options, dump, pass

---

## Practice Checklist

### Directory Structure Understanding
- [ ] Understand the purpose of all root directories (`/bin`, `/etc`, `/var`, etc.)
- [ ] Know the difference between static and variable data
- [ ] Understand shareable vs unshareable directories
- [ ] Locate configuration files in `/etc`
- [ ] Find log files in `/var/log`

### File System Management
- [ ] Display disk usage with `df` and `du`
- [ ] List block devices with `lsblk`
- [ ] Identify file system types with `blkid`
- [ ] Create partitions with `fdisk` or `parted`
- [ ] Create file systems with `mkfs`
- [ ] Mount file systems manually
- [ ] Configure persistent mounts in `/etc/fstab`
- [ ] Unmount file systems properly

### Disk Operations
- [ ] Add a new disk to the system
- [ ] Create partitions on the new disk
- [ ] Create a file system on the partition
- [ ] Mount the file system persistently
- [ ] Verify mount with `df` and `mount`

### System Information
- [ ] Check system information with `uname`
- [ ] Monitor disk space usage
- [ ] Check inode usage
- [ ] View and monitor log files
- [ ] Check kernel messages with `dmesg`

### Troubleshooting
- [ ] Troubleshoot mount failures
- [ ] Check and repair file systems with `fsck`
- [ ] Identify disk space issues
- [ ] Find large files consuming disk space
- [ ] Analyze log files for errors

---

## 📚 Additional Resources

### Important Files to Study
```
/etc/fstab          # Mount configuration
/etc/mtab           # Currently mounted file systems
/proc/mounts        # Mount information
/var/log/messages   # System logs
/var/log/secure     # Security logs
/etc/default/grub   # GRUB bootloader configuration
```

### Useful Commands for Practice
```bash
# Explore file system
tree / -L 1        # View directory structure (install tree package)

# Find configuration files
find /etc -name "*.conf"

# Monitor system
watch -n 1 df -h   # Watch disk usage changes

# Analyze disk usage
ncdu /             # Interactive disk usage (install ncdu)
```

