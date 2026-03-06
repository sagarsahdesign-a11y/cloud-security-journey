# 🐧 Linux Learning Journey

**Goal:** Master Linux fundamentals for Cloud Security Engineering  
**Duration:** 4 weeks (Feb - Mar 2026)  
**Progress:** Module 3 Complete ✅

---

## 📚 What I'm Learning

Following a structured path to learn Linux commands essential for cloud security roles. This repository tracks my progress and serves as a quick reference guide.

---

## ✅ Completed Modules

### Module 3: System Access and File System (Feb 19-Mar 4)

**Topics Covered:**
- File system structure and navigation
- Absolute vs relative paths
- Creating, finding, and organizing files
- Wildcards for pattern matching
- Soft and hard links

**Commands Mastered:**

#### Navigation Commands
```bash
pwd                     # Print working directory (shows current location)
ls                      # List files and directories
ls -l                   # Detailed list with permissions and sizes
ls -la                  # List all files including hidden ones
ls -ltr                 # List sorted by time (newest last)
cd <directory>          # Change to specified directory
cd ..                   # Go up one level
cd ~                    # Go to home directory
cd -                    # Go to previous directory
mkdir <name>            # Create new directory
mkdir -p path/to/dir    # Create nested directories
```

#### File Operations
```bash
touch <file>            # Create empty file
cat <file>              # Display file contents
echo "text" > file      # Write to file (overwrites)
echo "text" >> file     # Append to file
rm <file>               # Remove file
rm -i <file>            # Remove with confirmation prompt
cp <source> <dest>      # Copy file
cp -r <dir> <dest>      # Copy directory recursively
mv <source> <dest>      # Move or rename file
```

#### File Permissions (chmod)
```bash
chmod 755 <file>        # rwxr-xr-x (owner: all, group/others: read+execute)
chmod 644 <file>        # rw-r--r-- (owner: read+write, others: read only)
chmod 600 <file>        # rw------- (owner: read+write only)
chmod 000 <file>        # --------- (no permissions)

# Symbolic notation
chmod u+x <file>        # Add execute for user
chmod g-w <file>        # Remove write from group
chmod a+r <file>        # Add read for all (user+group+others)
chmod u+rwx <file>      # Give user all permissions
```

**Permission Numbers:**
- `7` = rwx (read + write + execute)
- `6` = rw- (read + write)
- `5` = r-x (read + execute)
- `4` = r-- (read only)
- `0` = --- (no permissions)

#### User Management
```bash
whoami                  # Show current user
id <username>           # Show user ID and groups
sudo groupadd <name>    # Create new group
sudo adduser <name>     # Create user (interactive)
sudo useradd -m -g <group> <user>  # Create user with specific group
ls /home                # List all user home directories
```

#### Finding Files
```bash
find . -name "*.txt"    # Find all .txt files in current directory
find /home -name <file> # Find file in /home directory
find . -type f          # Find only files
find . -type d          # Find only directories
locate <filename>       # Fast search using database (requires updatedb)
```

#### Wildcards
```bash
ls *.txt                # All files ending with .txt
ls file?.txt            # file1.txt, fileA.txt (single character)
ls file[123].txt        # file1.txt, file2.txt, file3.txt
rm file*                # Remove all files starting with 'file'
```

#### Links
```bash
# Hard Link (same inode, file data shared)
ln <source> <link>      # Create hard link
ls -li                  # Show inode numbers

# Soft Link (symbolic link, like shortcut)
ln -s <source> <link>   # Create soft link
```

**Key Difference:**
- **Hard link:** If original deleted, link still works
- **Soft link:** If original deleted, link breaks

#### Help Commands
```bash
man <command>           # View manual page
<command> --help        # Quick help summary
type <command>          # Check if builtin or external command
```

---

## 🎯 Key Concepts Learned

### Absolute vs Relative Paths

**Absolute Path** (starts with `/`)
- Always works from anywhere
- Example: `/home/Sagar/documents/file.txt`

**Relative Path** (no leading `/`)
- Depends on current location
- Example: `documents/file.txt`

### File Permission Format

```
-rwxr-xr-x
│││││││││└─ Others: execute
││││││││└── Others: write
│││││││└─── Others: read
││││││└──── Group: execute
│││││└───── Group: write
││││└────── Group: read
│││└─────── User: execute
││└──────── User: write
│└───────── User: read
└────────── File type (- = file, d = directory, l = link)
```

### Hidden Files
- Files starting with `.` are hidden
- View with `ls -a`
- Common examples: `.bashrc`, `.profile`, `.ssh/`

---

## 📝 Practice Exercises Completed

**Exercise 1: File System Navigation**
```bash
pwd                     # Check location
cd /tmp                 # Go to /tmp
ls -la                  # List all files
cd ~                    # Return home
```

**Exercise 2: Hard Links**
```bash
touch hulk
echo "hulk is a superhero" > hulk
ln hulk hulk-hardlink   # Create hard link
ls -li hulk*            # Check inodes (same number!)
rm hulk                 # Delete original
cat hulk-hardlink       # Still works! ✅
```

**Exercise 3: Permissions Practice**
```bash
touch sam
chmod 755 sam           # rwxr-xr-x
chmod 644 sam           # rw-r--r--
chmod 000 sam           # ---------
chmod 600 sam           # rw-------
```

---

## 🚀 What's Next

**Upcoming Modules:**
- [x] Module 3: System Access and File System
- [ ] Module 4: File Permissions & Text Processing (grep, awk, cut)
- [ ] Module 5: System Administration (processes, monitoring, logs)
- [ ] Module 6: Shell Scripting Basics

**Target Completion:** March 15, 2026

---

## 💡 Tips & Tricks

1. **Tab Completion:** Press TAB to auto-complete file/folder names
2. **Command History:** Press UP arrow to recall previous commands
3. **Clear Screen:** Type `clear` or press `Ctrl+L`
4. **Stop Command:** Press `Ctrl+C`
5. **Always double-check before `rm -rf`** — deletion is permanent!

---

## 📖 Resources Used

- LabEx Interactive Labs
- Linux Journey (linuxjourney.com)
- Kali Linux WSL (practice environment)
- Manual pages (`man` command)

---

## 🎓 Learning Approach

**Daily Routine:**
- Watch video tutorials (theory)
- Practice commands in Kali terminal
- Document new commands learned
- Update GitHub with progress

**Key Principle:** Type every command yourself — no copy-paste while learning!

---

## 📌 Notes to Self

- Linux is **case-sensitive**: `File.txt` ≠ `file.txt`
- Absolute paths start with `/`, relative paths don't
- `cp` copies, `mv` moves (original disappears)
- Hard links share data, soft links are shortcuts
- Practice daily — consistency beats intensity!

---

**Last Updated:** March 6, 2026  
**Next Session:** Module 4 - File Permissions & Text Processing
