//Linux move 
# RHCSA Commands Guide: cp, mv, touch, awk

## 1. cp - Copy Files and Directories

### Basic Syntax
```bash
cp [options] source destination
```

### Essential RHCSA Options

| Option | Description | Exam Importance |
|--------|-------------|-----------------|
| `-r` | Copy directories recursively | **High** |
| `-i` | Interactive (prompt before overwrite) | Medium |
| `-p` | Preserve permissions, ownership, timestamps | Medium |
| `-a` | Archive mode (preserve all attributes) | High |
| `-v` | Verbose output | Low |

### Exam-Ready Examples
```bash
# Copy file to another location
cp file1.txt /backup/

# Copy directory with all contents (must use -r)
cp -r /home/user/documents /backup/

# Copy preserving permissions (critical for system files)
cp -p /etc/hosts /backup/hosts.bak

# Interactive copy - prevents accidental overwrites
cp -i important.conf /etc/

# Copy multiple files to directory
cp file1.txt file2.txt file3.txt /destination/
```

### ⚠️ RHCSA Tip
> Always verify critical file copies with `ls -l` to confirm permissions are preserved when using `-p` .

---

## 2. mv - Move/Rename Files and Directories

### Basic Syntax
```bash
mv [options] source destination
```

### Essential RHCSA Options

| Option | Description |
|--------|-------------|
| `-i` | Interactive (prompt before overwrite) |
| `-f` | Force move (no prompt) |
| `-v` | Verbose output |
| `-n` | No overwrite existing files |

### Exam-Ready Examples

#### Rename Files
```bash
# Rename a file
mv oldname.txt newname.txt

# Rename a directory
mv old_directory new_directory
```

#### Move Files
```bash
# Move single file
mv file.txt /home/user/documents/

# Move multiple files to directory
mv file1.txt file2.txt file3.txt /destination/

# Move all files with same extension
mv *.log /var/log/archive/

# Move all files using wildcard
mv * /backup/           # All non-hidden files
```

#### Move All Files Including Hidden
```bash
# Move all files (including hidden)
mv {*,.*} /destination/ 2>/dev/null
```

### ⚠️ RHCSA Tip
> Unlike `cp`, `mv` does not duplicate files—it's like "cut and paste." Use `-i` to prevent accidental overwrites of important configuration files .

---

## 3. touch - Create Files and Update Timestamps

### Basic Syntax
```bash
touch [options] filename
```

### Essential RHCSA Options

| Option | Description |
|--------|-------------|
| `-a` | Change only access time |
| `-m` | Change only modification time |
| `-t` | Use specified timestamp |

### Exam-Ready Examples

#### Create Files
```bash
# Create empty file
touch file.txt

# Create multiple files at once
touch file1.txt file2.txt file3.txt

# Create files using sequence
touch file{1..10}.txt

# Create files with different extensions
touch file{1..5}.{txt,log,conf}
```

#### Update Timestamps
```bash
# Update timestamp of existing file
touch existing_file.txt

# Create file with specific timestamp
touch -t 202403251200 backup.txt
```

### 💡 Pro Tip
> `touch` is also useful for creating placeholder files or forcing log file rotation by updating timestamps .

---

## 4. awk - Text Processing

### Basic Syntax
```bash
awk 'pattern {action}' file
```

### Essential RHCSA Patterns

#### Print Specific Columns
```bash
# Print first column
awk '{print $1}' file.txt

# Print first and third columns
awk '{print $1, $3}' file.txt

# Print last column
awk '{print $NF}' file.txt
```

#### Pattern Matching
```bash
# Find lines containing "error"
awk '/error/ {print}' /var/log/messages

# Print lines where column 3 equals "active"
awk '$3 == "active"' status.txt

# Print lines where column 2 > 100
awk '$2 > 100' data.txt
```

#### Field Separator
```bash
# Parse /etc/passwd (colon-separated)
awk -F: '{print $1, $3}' /etc/passwd

# Parse CSV files
awk -F, '{print $2, $4}' data.csv
```

#### Built-in Variables

| Variable | Description |
|----------|-------------|
| `NR` | Current line number |
| `NF` | Number of fields |
| `$0` | Entire line |
| `FS` | Field separator |

### Exam-Ready Examples
```bash
# Extract usernames from passwd file
awk -F: '{print $1}' /etc/passwd

# Print lines 5-10 of a file
awk 'NR>=5 && NR<=10' file.txt

# Calculate total of column
awk '{sum += $1} END {print "Total:", sum}' numbers.txt

# Count lines containing pattern
awk '/failed/ {count++} END {print count}' /var/log/secure

# Format output neatly
awk '{printf "%-15s %5d\n", $1, $2}' data.txt
```

---

## 📝 RHCSA Practice Tasks

### Task 1: File Operations
```bash
# 1. Create directory structure
mkdir -p /tmp/rhcsa/{docs,backup,logs}

# 2. Create multiple files
touch /tmp/rhcsa/docs/file{1..5}.txt

# 3. Copy files with permissions preserved
cp -rp /tmp/rhcsa/docs /tmp/rhcsa/backup/

# 4. Move all .txt files to logs directory
mv /tmp/rhcsa/docs/*.txt /tmp/rhcsa/logs/

# 5. Rename a file
mv /tmp/rhcsa/logs/file1.txt /tmp/rhcsa/logs/backup.txt
```

### Task 2: Text Processing with awk
```bash
# Given /etc/passwd, extract:
# 1. List all usernames
awk -F: '{print $1}' /etc/passwd

# 2. Find users with UID > 1000
awk -F: '$3 > 1000 {print $1, $3}' /etc/passwd

# 3. Count number of users
awk -F: 'END {print "Total users:", NR}' /etc/passwd
```

---

## 🔍 Quick Reference Card

| Command | Purpose | Exam-Ready Syntax |
|---------|---------|-------------------|
| `cp` | Copy files | `cp -rp source dest` |
| `mv` | Move/rename | `mv -i source dest` |
| `touch` | Create/update | `touch file{1..10}.txt` |
| `awk` | Text processing | `awk -F: '{print $1}' /etc/passwd` |

