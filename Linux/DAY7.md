You're absolutely right! Here's the content formatted as a proper `README.md` file with proper markdown formatting:

```markdown
# RHCSA Study Notes

A comprehensive guide for Red Hat Certified System Administrator (RHCSA) exam preparation covering essential system administration tasks.

## Table of Contents

- [File Management Commands](#file-management-commands)
- [User Management](#user-management)
- [Group Management](#group-management)
- [Important Files Locations](#important-files-locations)
- [Key Commands Summary](#key-commands-summary)
- [Quick Reference Tips](#quick-reference-tips)
- [Practice Checklist](#practice-checklist)

---

## File Management Commands

### Sort Command Examples

```bash
# Basic sort
sort file1.txt

# Numeric sort
sort -n nums.doc

# Sort unique lines only
sort -u data.txt

# Sort by specific column
sort -k2 data1.txt      # Sort by column 2
sort -k1 data1.txt      # Sort by column 1
sort -k1,2 data1.txt    # Sort by columns 1 and 2

# Sort by month
sort -M month.txt
```

**💡 Tips:**
- `-n` is essential for numeric sorting, otherwise numbers are sorted alphabetically
- `-u` removes duplicates while sorting
- `-k` allows sorting by specific fields
- `-M` sorts months (JAN, FEB, etc.) correctly

---

## User Management

### User Types and UID Ranges

| User Type | RHEL 7,8,9 | RHEL 5-6 |
|-----------|------------|----------|
| **Privileged User** | 0-199 | 0-199 |
| **System Users** | 201-999 | 201-499 |
| **Normal Users** | 1000-60000 | 500-60000 |

**🔑 Key Points:**
- **Root (UID 0)**: Superuser with unlimited privileges (`#` prompt)
- **System Users**: Service accounts for daemons and services
- **Normal Users**: Regular user accounts with limited privileges (`$` prompt)

### `/etc/passwd` File Structure (7 Fields)

| Field | Description | Example |
|-------|-------------|---------|
| 1 | Username | `john` |
| 2 | Password mask | `x` (password in `/etc/shadow`) |
| 3 | User ID (UID) | `1000` |
| 4 | Group ID (GID) | `1000` |
| 5 | GECOS (Full name) | `John Doe` |
| 6 | Home directory | `/home/john` |
| 7 | Login shell | `/bin/bash` |

### User Management Commands

#### Adding Users

```bash
# Basic user addition
useradd username

# With specific UID
useradd -u 222 ram

# Set password
passwd username
```

#### Modifying Users (usermod)

```bash
usermod -u 111 username           # Change UID
usermod -g 100 username           # Change primary group (GID)
usermod -c "Full Name" username   # Change GECOS/description
usermod -d /new/home username     # Change home directory
usermod -s /sbin/nologin username # Change shell
usermod -l newname username       # Change login name
```

**⚠️ Important Notes:**
- Home directory changes should be done carefully
- Setting shell to `/sbin/nologin` prevents user from logging in
- Always verify changes with `cat /etc/passwd`

### User Management Practice Examples

```bash
# Create user with specific UID
useradd -u 2222 shyam

# Modify user properties
usermod -u 111 unnati
usermod -g 100 unnati
usermod -c manager unnati
usermod -s /sbin/nologin unnati
usermod -l prac unnati
```

---

## Group Management

### Group Files Location
- **Configuration**: `/etc/group`

### `/etc/group` File Structure (4 Fields)

| Field | Description | Example |
|-------|-------------|---------|
| 1 | Group name | `developers` |
| 2 | Password mask | `x` |
| 3 | Group ID (GID) | `1000` |
| 4 | Member list | `user1,user2` |

### Group Types

| Type | Description | Option |
|------|-------------|--------|
| **Primary Group** | Every user has one primary group | `-g` |
| **Secondary Group** | Users can be members of multiple groups | `-G` |

### Group Management Commands

```bash
# Create groups
groupadd mygroup
groupadd linux

# Check groups
cat /etc/group
id username    # Show user's group memberships

# Add user to secondary group
usermod -G linux myuser        # Overwrites existing groups
usermod -aG linux myuser       # Appends to existing groups
```

**⚠️ Critical Note:**
- `-G` overwrites existing secondary group memberships
- `-aG` appends to secondary groups (preserves existing)
- Always verify with `id username` after changes

### Group Management Practice Example

```bash
groupadd mygroup
groupadd linux
useradd myuser
passwd myuser
id myuser
usermod -G linux myuser
cat /etc/group
usermod -G mygroup myuser
cat /etc/group
usermod -aG linux myuser
id myuser
```

---

## Important Files Locations

| File | Purpose | View Command |
|------|---------|--------------|
| `/etc/passwd` | User account information | `cat /etc/passwd` |
| `/etc/group` | Group information | `cat /etc/group` |
| `/etc/shadow` | Encrypted passwords (root only) | `sudo cat /etc/shadow` |
| `/etc/default/useradd` | Default useradd settings | `cat /etc/default/useradd` |
| `/etc/login.defs` | System-wide login settings | `cat /etc/login.defs` |

---

## Key Commands Summary

### File Operations
| Command | Description |
|---------|-------------|
| `sort [options] [file]` | Sort file content |
| `cat [file]` | Display file content |
| `vi [file]` | Edit file with Vim |
| `clear` | Clear terminal screen |
| `history` | Show command history |

### User Operations
| Command | Description |
|---------|-------------|
| `useradd [options] [username]` | Add new user |
| `usermod [options] [username]` | Modify existing user |
| `passwd [username]` | Set/change user password |
| `id [username]` | Show user ID and group memberships |

### Group Operations
| Command | Description |
|---------|-------------|
| `groupadd [groupname]` | Add new group |
| `groupmod [options] [groupname]` | Modify existing group |

---

## Quick Reference Tips

### 🎯 User Management Best Practices

1. **Always verify changes:**
   ```bash
   cat /etc/passwd | grep username
   cat /etc/group | grep groupname
   id username
   ```

2. **Use `-aG` instead of `-G`** to preserve existing secondary group memberships

3. **System users** should have `/sbin/nologin` shell for security

4. **UID ranges** are important for distinguishing user types

5. **Check defaults before creating users:**
   ```bash
   cat /etc/default/useradd
   ```

### 📝 Common Interview Questions

1. **What are the 7 fields in `/etc/passwd`?**
   - Username, password mask, UID, GID, GECOS, home directory, shell

2. **Difference between `-g` and `-G` in user management?**
   - `-g`: Sets primary group
   - `-G`: Sets secondary group(s)

3. **What's the difference between `usermod -G` and `usermod -aG`?**
   - `-G`: Overwrites all secondary groups
   - `-aG`: Appends to existing secondary groups

4. **Explain user UID ranges in RHEL:**
   - 0-199: Privileged/System users
   - 201-999: System users (RHEL 7+)
   - 1000+: Normal users

### 🔍 Verification Commands

```bash
# Always verify after making changes
cat /etc/passwd | grep username
cat /etc/group | grep groupname
id username
grep username /etc/passwd
grep groupname /etc/group
```

---

## Practice Checklist

### File Management
- [ ] Sort files with different options (`-n`, `-u`, `-k`)
- [ ] Sort by specific columns
- [ ] Sort month data correctly

### User Management
- [ ] Create users with different UIDs
- [ ] Modify user properties (UID, GID, shell, home directory)
- [ ] Change user login names
- [ ] Set GECOS/description for users
- [ ] Verify changes in `/etc/passwd`

### Group Management
- [ ] Create new groups
- [ ] Add users to primary groups
- [ ] Add users to secondary groups using `-G`
- [ ] Add users to secondary groups using `-aG`
- [ ] Understand the difference between `-G` and `-aG`
- [ ] Verify group memberships with `id` command

### Verification
- [ ] Check all user configurations
- [ ] Verify group memberships
- [ ] Understand UID ranges for different RHEL versions

