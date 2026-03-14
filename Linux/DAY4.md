Here are well-organized notes from your terminal history, with each command's purpose explained and additional key points added.

---

## **Day 4 & 5 - Linux Commands Notes**

### **1. `mv` Command (Move/Rename)**
**Use:** Moves files or directories from one location to another. Also used to rename files/directories.

**Syntax:**
```bash
mv source destination
```

**Example:**
```bash
mv file1.txt /home/user/Documents/    # Move file to another directory
mv oldname.txt newname.txt            # Rename file
```

**Key Points:**
- Can move single files, multiple files, or entire directories
- If destination is an existing directory, source is moved inside it
- If destination doesn't exist, source is renamed to destination

---

### **2. `cat` Command (Concatenate)**
**Use:** Displays the contents of a file on the terminal.

**Syntax:**
```bash
cat filename
```

**Example:**
```bash
cat implementation_plan.md     # Display file content
```

**Key Points:**
- Can display multiple files: `cat file1 file2`
- Can create files: `cat > newfile.txt`
- Can append to files: `cat >> existingfile.txt`

---

### **3. `grep` Command (Global Regular Expression Print)**
**Use:** Searches for patterns/strings within files.

**Syntax:**
```bash
grep [options] pattern filename
```

**Common Options Used:**
| Option | Description |
|--------|-------------|
| `-i` | Ignore case (case-insensitive search) |
| `-o` | Show only the matching part, not the whole line |
| `-c` | Count number of matching lines |
| `-w` | Match whole word only |
| `^pattern` | Lines starting with pattern |
| `pattern$` | Lines ending with pattern |

**Examples from History:**
```bash
grep server implementation_plan.md        # Search for "server"
grep -i system implementation_plan.md     # Case-insensitive search
grep -io system implementation_plan.md    # Case-insensitive, show only matches
grep ^sys implementation_plan.md          # Lines starting with "sys"
grep sys$ implementation_plan.md          # Lines ending with "sys"
grep sys implementation_plan.md -c        # Count occurrences
grep sys implementation_plan.md -w        # Match whole word "sys"
```

**Key Points:**
- Can search multiple files: `grep pattern file1 file2`
- Supports regular expressions for complex pattern matching
- Very useful for filtering log files and finding specific information

---

### **4. `cut` Command**
**Use:** Extracts specific sections/columns from each line of a file.

**Syntax:**
```bash
cut [options] filename
```

**Common Options:**
| Option | Description |
|--------|-------------|
| `-d` | Delimiter (character that separates fields) |
| `-f` | Field number(s) to extract |
| `-c` | Character position(s) to extract |

**Examples from History:**
```bash
cut -d : -f1 /etc/passwd                 # Extract first field (username)
cut -d : -f1-4 /etc/passwd               # Extract fields 1 through 4
cut -d : -f6-7 /etc/passwd                # Extract fields 6 through 7
cut -d : -f1,3,5 /etc/passwd              # Extract fields 1, 3, and 5
cut -c 8 /etc/passwd                      # Extract 8th character of each line
cut -c 20-25 /etc/passwd                   # Extract characters 20 to 25
cut -c -25 /etc/passwd                     # Extract first 25 characters
cut -c 25- /etc/passwd                     # Extract from character 25 to end
```

**Key Points:**
- Default delimiter is TAB (use `-d` to change)
- Perfect for parsing structured data like CSV files, system files
- Often combined with `grep` and other commands using pipes

---

### **5. Pipe (`|`) and `nl`, `wc` Commands**

**Pipe (`|`):** Connects commands - output of first becomes input of second

**Examples:**
```bash
cut -d : -f1 /etc/passwd | wc             # Count lines, words, chars of output
cut -d : -f1 /etc/passwd | nl             # Add line numbers to output
cut -d : -f6-7 /etc/passwd | grep nologin # Find lines containing "nologin"
```

**Key Points:**
- `wc` (word count): counts lines, words, characters
- `nl` (number lines): displays file with line numbers

---

### **6. `sed` Command (Stream Editor)**
**Use:** Performs text transformations on a file/stream without opening in an editor.

**Syntax:**
```bash
sed [options] 'command' filename
```

**Creating a Test File with `vi`:**
```bash
vi myfile          # Open vi editor
# Press 'i' to enter insert mode
# Type or paste content
# Press ESC, then :wq to save and quit
```

**Common `sed` Operations:**

| Command | Description |
|---------|-------------|
| `s/old/new/` | Substitute (replace) first occurrence per line |
| `s/old/new/g` | Global substitute (replace all occurrences) |
| `3s/old/new/g` | Substitute only on line 3 |
| `2,4s/old/new/` | Substitute on lines 2 through 4 |
| `5d` | Delete line 5 |
| `/pattern/d` | Delete lines containing pattern |

**Examples from History:**
```bash
sed 's/server/linux/4' myfile        # Replace 4th occurrence of "server" per line
sed 's/server/linux/2' myfile        # Replace 2nd occurrence per line
sed 's/server/linux/g' myfile         # Replace ALL occurrences globally
sed '3s/server/linux/g' myfile        # Global replace only on line 3
sed '3s/server/linux/6' myfile        # Replace 6th occurrence on line 3 only
sed '2,4s/server/linux/2' myfile      # Replace 2nd occurrence on lines 2-4
sed '2,7s/server/linux/2' myfile      # Replace 2nd occurrence on lines 2-7
sed '5d' myfile                        # Delete line 5
sed '/server/d' myfile                 # Delete all lines containing "server"
```

**Key Points:**
- Original file remains unchanged unless you use `-i` option
- `sed -i` will make changes directly to the file
- Can combine multiple commands with `-e`
- Extremely powerful for batch editing and scripting

---

## **Important Terminology**

| Term | Description |
|------|-------------|
| **Delimiter** | A character used to separate fields (like `:` in `/etc/passwd`) |
| **Field** | A column or piece of data separated by delimiters |
| **Pattern** | The text or regular expression you're searching for |
| **Stream** | Data that flows from one command to another |
| **Pipe** | The `|` symbol that connects command outputs to inputs |
| **Substitution** | Replacing one text pattern with another |

---

## **Command Summary Table**

| Command | Primary Use | Common Options |
|---------|-------------|----------------|
| `mv` | Move/rename files | - |
| `cat` | Display file content | - |
| `grep` | Search text | `-i`, `-o`, `-c`, `-w` |
| `cut` | Extract columns | `-d`, `-f`, `-c` |
| `sed` | Stream editing | `s///`, `d` |
| `wc` | Word count | - |
| `nl` | Number lines | - |
| `vi` | Text editor | `i`, `:wq` |

---

## **Pro Tips**
- Combine commands with pipes for powerful data processing:
  ```bash
  cut -d : -f1 /etc/passwd | grep root | nl
  ```
- Always test `sed` commands without `-i` first to see what will change
- Use `history` command (like you did with #931) to review previous commands
- `grep` is case-sensitive by default - use `-i` when case doesn't matter