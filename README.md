# 🐧 Linux Learning Journey

**Goal:** Master Linux fundamentals for Cloud Security Engineering  
**Duration:** 4 weeks (Feb - Mar 2026)  
**Progress:** Module 4 Complete ✅

---

## 📚 What I'm Learning

Following a structured path to learn Linux commands essential for cloud security roles. This repository tracks my progress and serves as a quick reference guide.

---

## ✅ Completed Modules

### Module 3: System Access and File System (Feb 19 - Mar 4)

**Topics Covered:**
- File system structure and navigation
- Absolute vs relative paths
- Creating, finding, and organizing files
- Wildcards for pattern matching
- Soft and hard links

**Commands Mastered:**

#### Navigation Commands
```
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
```
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
```
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
```
whoami                  # Show current user
id <username>           # Show user ID and groups
sudo groupadd <name>    # Create new group
sudo adduser <name>     # Create user (interactive)
sudo useradd -m -g <group> <user>  # Create user with specific group
ls /home                # List all user home directories
```

#### Finding Files
```
find . -name "*.txt"    # Find all .txt files in current directory
find /home -name <file> # Find file in /home directory
find . -type f          # Find only files
find . -type d          # Find only directories
locate <filename>       # Fast search using database (requires updatedb)
```

#### Wildcards
```
ls *.txt                # All files ending with .txt
ls file?.txt            # file1.txt, fileA.txt (single character)
ls file[123].txt        # file1.txt, file2.txt, file3.txt
rm file*                # Remove all files starting with 'file'
```

#### Links
```
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
```
man <command>           # View manual page
<command> --help        # Quick help summary
type <command>          # Check if builtin or external command
```

---

### Module 4: File Ownership, Permissions & Text Operations (Mar 6 - Mar 10)

**Topics Covered:**
- File ownership with `chown` and `chgrp`
- Access Control Lists (ACL) with `getfacl` and `setfacl`
- Input/Output redirects (`>`, `>>`, `<`, `2>`)
- Standard output to multiple files with `tee`
- Pipes (`|`) to chain commands
- File maintenance: `cp`, `mv`, `rm`, `mkdir`, `rmdir`
- File display: `cat`, `more`, `less`, `head`, `tail`

**Commands Mastered:**

#### File Ownership
```
chown <user> <file>          # Change owner of file
chown <user>:<group> <file>  # Change owner AND group together
chgrp <group> <file>         # Change group of file

# Examples (must be root/sudo)
sudo chown root sam          # Change owner to root
sudo chgrp root sam          # Change group to root
sudo chown sagar:sagar file  # Reset both owner and group to sagar
```

**Key notes:**
- Only root or `sudo` can change ownership
- Regular users CANNOT change group to one they don't belong to
- Verified with `ls -l` — shows `owner group` in columns 3 and 4

#### Access Control Lists (ACL)
```
# Install ACL tools first
sudo apt install acl -y

getfacl <file>               # View ACL permissions on a file
setfacl -m u:<user>:<perms> <file>   # Add/modify user ACL
setfacl -m g:<group>:<perms> <file>  # Add/modify group ACL
setfacl -x u:<user> <file>  # Remove specific user ACL entry
setfacl -b <file>            # Remove ALL ACL entries (back to default)

# Example
setfacl -m u:sagar:rw /tmp/tx    # Give sagar read+write on tx
setfacl -m g:sagar:rw /tmp/tx    # Give sagar's group read+write on tx
getfacl /tmp/tx                  # View all ACL entries
```

**ACL Output Example:**
```
# file: tmp/tx
# owner: root
# group: root
user::rw-
user:sagar:rw-       ← extra user permission
group::r--
group:sagar:rw-      ← extra group permission
mask::rw-
other::r--
```

**Why use ACL?** — Standard chmod only allows one user/group. ACL lets you grant permissions to additional specific users without changing ownership.

#### Input/Output Redirects
```
# Standard Output redirect
command > file          # Redirect output to file (OVERWRITES)
command >> file         # Append output to file (keeps existing content)

# Standard Input redirect
command < file          # Use file as input instead of keyboard

# Standard Error redirect
command 2> file         # Redirect error messages to file

# Examples
ls -ltr > listing       # Save ls output into listing file
date >> sagar           # Append current date to sagar file
pwd > findpath          # Save current path to findpath file
ls -l /root 2> errorfile   # Save permission denied error to errorfile
cat < findpath          # Read findpath as input to cat
```

**The three streams:**
| Stream | Number | Symbol | Description |
|--------|--------|--------|-------------|
| stdin  | 0      | `<`    | Standard Input (keyboard) |
| stdout | 1      | `>`    | Standard Output (screen) |
| stderr | 2      | `2>`   | Standard Error (screen) |

#### tee Command (Output to Screen AND File)
```
tee <file>              # Write stdin to both screen and file (overwrites)
tee -a <file>           # Append to file instead of overwrite
tee file1 file2 file3   # Write to multiple files simultaneously

# Using with pipes
echo "text" | tee myfile           # Show on screen AND save to file
ls -l | tee listdir                # Save ls output to file, still see it
echo "more text" | tee -a myfile   # Append to file
ls -l | tee file1 file2 file3      # Copy output to 3 files at once
```

**Difference from `>`:**
- `>` sends output ONLY to file (you don't see it on screen)
- `tee` sends output to BOTH screen and file at the same time

#### Pipes
```
command1 | command2     # Send output of command1 as input to command2

# Examples
ls -ltr | more          # Page through long directory listing
ls -l | tail -1         # Show only the last line of ls output
ls -ltr | grep "sagar"  # Filter ls output to lines containing "sagar"
cat file | wc -l        # Count lines in a file
```

**How pipes work:** The `|` takes stdout of the left command and feeds it as stdin to the right command — no temporary files needed.

#### File Display Commands
```
cat <file>              # Show entire file content at once
more <file>             # Page through file (spacebar=next page, q=quit)
less <file>             # Page through file (scroll up/down, q=quit)
head <file>             # Show first 10 lines
head -n 5 <file>        # Show first 5 lines
tail <file>             # Show last 10 lines
tail -n 5 <file>        # Show last 5 lines
tail -f <file>          # Follow file in real time (useful for logs)
wc -c <file>            # Count characters/bytes in file
wc -l <file>            # Count lines in file
wc -w <file>            # Count words in file
```

**When to use which:**
- `cat` — short files, quick view
- `more/less` — long files like `/etc` directory listing
- `head/tail` — check beginning or end of log files
- `tail -f` — watch live logs in real time

#### File Maintenance Commands
```
cp <source> <dest>      # Copy file (keeps original)
cp <file> /path/to/dir  # Copy file to a different directory

mv <source> <dest>      # Move OR rename file (original disappears)
mv <file> /path/to/dir  # Move file to a different directory

rm <file>               # Delete file (permanent!)
rm -r <directory>       # Delete directory and all contents

mkdir <dirname>         # Create new empty directory
rmdir <dirname>         # Remove empty directory only
rm -r <dirname>         # Remove directory even if it has files
```

**cp vs mv:**
- `cp john david` — john still exists, david is a new copy
- `mv lex luther` — lex is gone, now called luther
- `mv warner /tmp` — file physically moves to /tmp folder

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

### Why Ownership Matters for Security
- Files in `/etc` are owned by root — regular users can't modify them
- `sam` file owned by root in `/home/sagar` — sagar can't delete it even from their own home!
- This is intentional: protects system files from accidental/malicious modification

---

## 📝 Practice Exercises Completed

**Exercise 1: File System Navigation**
```
pwd                     # Check location
cd /tmp                 # Go to /tmp
ls -la                  # List all files
cd ~                    # Return home
```

**Exercise 2: Hard Links**
```
touch hulk
echo "hulk is a superhero" > hulk
ln hulk hulk-hardlink   # Create hard link
ls -li hulk*            # Check inodes (same number!)
rm hulk                 # Delete original
cat hulk-hardlink       # Still works! ✅
```

**Exercise 3: Permissions Practice**
```
touch sam
chmod 755 sam           # rwxr-xr-x
chmod 644 sam           # rw-r--r--
chmod 000 sam           # ---------
chmod 600 sam           # rw-------
```

**Exercise 4: Ownership Practice**
```
sudo -i                         # Switch to root
chown root sam                  # Change owner to root
chgrp root sam                  # Change group to root
ls -ltr                         # Verify: -rw-rw-r-- 1 root root
chown sagar:sagar warner        # Reset both owner and group
```

**Exercise 5: ACL Practice**
```
touch /tmp/tx
getfacl /tmp/tx                 # Default ACL
setfacl -m u:sagar:rw /tmp/tx  # Add user ACL
setfacl -m g:sagar:rw /tmp/tx  # Add group ACL
setfacl -x u:sagar /tmp/tx     # Remove user ACL
setfacl -b /tmp/tx              # Remove all ACL
```

**Exercise 6: Redirects & Pipes**
```
ls -ltr > listing               # Save output to file
date >> sagar                   # Append date
ls -l /root 2> errorfile        # Capture error
echo "text" | tee myfile        # Screen + file
ls -ltr | more                  # Paginate output
```

**Exercise 7: File Maintenance**
```
cp john david                   # Copy file
cp david /tmp                   # Copy to different directory
mv lex luther                   # Rename file
mv warner /tmp                  # Move to /tmp
rm remove                       # Delete file
mkdir gameofwar                 # Create directory
rmdir gameofwar                 # Remove empty directory
rm -r gameofwar                 # Remove directory with contents
```

---

## 🚀 What's Next

**Upcoming Modules:**
- Module 5: Text Processing (`grep`, `cut`, `awk` basics)
- Module 6: System Administration (processes, monitoring, logs)
- Module 7: Shell Scripting Basics

**Target Completion:** March 15, 2026

---

## 💡 Tips & Tricks

1. **Tab Completion:** Press TAB to auto-complete file/folder names
2. **Command History:** Press UP arrow to recall previous commands
3. **Clear Screen:** Type `clear` or press `Ctrl+L`
4. **Stop Command:** Press `Ctrl+C`
5. **Always double-check before `rm -rf`** — deletion is permanent!
6. **`sudo -i` vs `su -`** — `sudo -i` is preferred in Kali; `su -` needs root password set
7. **`2>`** catches errors, `>` catches normal output — very useful for scripts!

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
- `>` overwrites, `>>` appends — don't mix them up!
- `tee` = pipe to screen AND file at the same time
- Regular users can't change ownership — need `sudo`
- Practice daily — consistency beats intensity!

---

**Last Updated:** March 10, 2026  
**Next Session:** Module 5 - Text Processing (grep, cut, awk)
