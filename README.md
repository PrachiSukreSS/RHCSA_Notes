# RHCSA Notes

A practical, command-focused study repository for preparing for the **Red Hat Certified System Administrator (RHCSA)** exam. The notes combine Linux administration explanations, terminal histories, practice exercises, exam reminders, screenshots, and reference material from hands-on RHEL 9 labs.

> **Disclaimer:** These notes are personal study material. Always verify commands against the current Red Hat documentation and test destructive operations in a disposable virtual machine before using them on a real system.

## What this repository covers

- Linux file and directory management
- User and group administration
- File permissions, ownership, `umask`, ACLs, SUID, SGID, and sticky bit
- File searching and text processing with `find`, `grep`, `cut`, `sed`, `awk`, `sort`, pipes, and redirection
- Processes, services, systemd targets, and boot flow
- Job scheduling with `at` and `cron`
- Disk partitioning, filesystems, mounting, swap, and `/etc/fstab`
- Logical Volume Manager (LVM): PVs, VGs, LVs, physical extents, and resizing
- Networking with NetworkManager, `nmcli`, `nmtui`, hostname configuration, and firewall basics
- NFS server/client configuration and automount concepts
- SELinux modes, contexts, and troubleshooting considerations
- SSH password-based and key-based access
- Package management with RPM, YUM, and DNF
- Podman and container fundamentals
- RHCSA-style practical tasks and exam-day reminders

## Repository layout

```text
.
├── Linux/
│   ├── Day3.md       # cp, mv, touch, awk, and file-operation practice
│   ├── DAY4.md       # Linux filesystem hierarchy and filesystem management
│   ├── Day5.md       # mv, cat, grep, cut, pipes, wc, nl, and sed
│   ├── Day6.md       # Placeholder for additional notes
│   └── DAY7.md       # User/group administration and RHCSA exam topics
├── IMages/
│   ├── File_System_Hierarchy.png
│   └── exam_session   # Password reset, targets, SELinux, storage, NTP, and exam notes
├── photos/
│   ├── create_space.png
│   ├── network_setup.png
│   ├── sudoers_file.png
│   ├── tar1.png
│   ├── tar2.png
│   ├── task2_ques.png
│   ├── zip1.png
│   └── zip2.png
├── Notes.txt           # User, group, permissions, sorting, and shell notes
├── NOtes2.txt          # Structured notes on special permissions and password troubleshooting
├── imp.txt             # Quick revision notes
├── notes3.txt          # at, cron, access restrictions, and SGID notes
├── notes4.txt          # umask, sudo, ACLs, find, links, processes, tar, zip, gzip, and bzip2
├── notes5.txt          # Boot process, partitions, swap, filesystems, and LVM practicals
├── notes6.txt          # Networking, firewalld, NFS, and autofs notes
├── notes7.txt          # SELinux and SSH notes
├── notes8.txt          # Podman and container fundamentals
├── notes9.txt          # Package-management overview
├── secure copy.pdf     # Supporting reference document
├── taask               # Partitioning and filesystem practical task
└── task2_ans           # LVM, filesystem, and persistent-mount command history
```

> The repository currently contains several files with inconsistent capitalization and names, such as `IMages`, `NOtes2.txt`, `taask`, and `Day3.md`. The names are preserved so existing links and references continue to work.

## Recommended study path

### 1. Build Linux fundamentals

Start with the command and file-operation notes:

- [`Linux/Day3.md`](Linux/Day3.md) — `cp`, `mv`, `touch`, and `awk`
- [`Linux/Day5.md`](Linux/Day5.md) — `cat`, `grep`, `cut`, pipes, `wc`, `nl`, and `sed`
- [`Notes.txt`](Notes.txt) — sorting, users, groups, permissions, and `usermod`

### 2. Learn identity and access management

Review:

- [`Linux/DAY7.md`](Linux/DAY7.md)
- [`NOtes2.txt`](NOtes2.txt)
- [`notes4.txt`](notes4.txt)

These notes cover `/etc/passwd`, `/etc/group`, user and group commands, ownership, standard permissions, `umask`, sudo access, ACLs, links, SUID, SGID, and sticky bit behavior.

### 3. Practice storage administration

Use:

- [`Linux/DAY4.md`](Linux/DAY4.md)
- [`notes5.txt`](notes5.txt)
- [`taask`](taask)
- [`task2_ans`](task2_ans)

The practical examples walk through partition tables, filesystems, swap, UUID-based mounts, `/etc/fstab`, LVM creation, physical extent sizing, and logical-volume expansion.

### 4. Study scheduling, networking, and services

Review:

- [`notes3.txt`](notes3.txt) — `at`, `cron`, `at.deny`, `cron.deny`, and SGID
- [`notes6.txt`](notes6.txt) — NetworkManager, firewalld, NFS, and autofs
- [`notes7.txt`](notes7.txt) — SELinux and SSH

### 5. Finish with packages and containers

- [`notes9.txt`](notes9.txt) — RPM, YUM, DNF, and other package managers
- [`notes8.txt`](notes8.txt) — Podman, images, containers, rootless operation, and basic commands

## Useful command areas

The repository provides examples for commands including:

```bash
# System and storage inspection
lsblk
blkid
df -hT
findmnt
free -h

# Users and groups
useradd username
passwd username
usermod -aG group username
id username

# Permissions and ownership
chmod 755 path
chown user:group path
getfacl path
setfacl -m u:username:rwx path

# Services and scheduling
systemctl status service
systemctl enable --now service
systemctl set-default multi-user.target
atq
crontab -e

# Filesystems and LVM
mkfs.xfs /dev/device
mount -a
pvcreate /dev/device
vgcreate volume_group /dev/device
lvcreate -L 1G -n logical_volume volume_group
```

Commands that modify disks, partitions, filesystems, boot configuration, permissions, networking, or authentication should be run only with appropriate privileges and after confirming the target device or path.

## Practice environment

The examples are written for Red Hat Enterprise Linux-style systems and frequently use `dnf`/`yum`, `systemd`, NetworkManager, `firewalld`, SELinux, LVM, and RHEL device names. A virtual machine is recommended for practice.

Suggested lab setup:

1. Use a RHEL-compatible virtual machine.
2. Create a non-production snapshot before storage or boot exercises.
3. Add one or more disposable virtual disks for partitioning and LVM practice.
4. Use two virtual machines for SSH and NFS exercises.
5. Verify every change with commands such as `lsblk`, `findmnt`, `df -hT`, `id`, `getenforce`, `systemctl status`, and `mount -a`.

## Notes and limitations

- Some files are raw command histories rather than polished tutorials; command order and context may depend on the original lab environment.
- A few examples contain typos or exploratory commands. Treat them as troubleshooting history, not blindly copyable production procedures.
- Device names such as `/dev/sda`, `/dev/sdb`, `/dev/loop1`, and IP addresses are environment-specific.
- The exact RHCSA objectives and exam procedures can change. Use the current official Red Hat exam objectives as the authoritative source.

## Contributing improvements

When improving the notes:

- Prefer Markdown files for new structured topics.
- Use descriptive, consistently capitalized filenames.
- Include the command purpose, syntax, example, expected verification, and cleanup steps.
- Clearly mark commands that can destroy data.
- Keep screenshots next to the topic that references them.
- Correct or annotate outdated commands instead of silently removing useful troubleshooting history.

## License

No license is currently declared for this repository. Unless a license is added, the content should be treated as “all rights reserved.”
