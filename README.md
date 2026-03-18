# 🐧 Linux Learning Journey

**Goal:** Master Linux fundamentals for Cloud Security Engineering  
**Duration:** 4 weeks (Feb - Mar 2026)  
**Progress:** Module 3 n 4 Completed ✅

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
```bash
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
```bash
sudo apt install acl -y

getfacl <file>                         # View ACL permissions on a file
setfacl -m u:<user>:<perms> <file>    # Add/modify user ACL
setfacl -m g:<group>:<perms> <file>   # Add/modify group ACL
setfacl -x u:<user> <file>            # Remove specific user ACL entry
setfacl -b <file>                     # Remove ALL ACL entries (back to default)

# Example
setfacl -m u:sagar:rw /tmp/tx         # Give sagar read+write on tx
setfacl -m g:sagar:rw /tmp/tx         # Give sagar's group read+write
getfacl /tmp/tx                        # View all ACL entries
```

**Why use ACL?** — Standard chmod only allows one user/group. ACL lets you grant permissions to additional specific users without changing ownership.

#### Input/Output Redirects
```bash
command > file          # Redirect output to file (OVERWRITES)
command >> file         # Append output to file (keeps existing)
command < file          # Use file as input instead of keyboard
command 2> file         # Redirect error messages to file
```

**The three streams:**

| Stream | Number | Symbol | Description |
|--------|--------|--------|-------------|
| stdin  | 0      | `<`    | Standard Input (keyboard) |
| stdout | 1      | `>`    | Standard Output (screen) |
| stderr | 2      | `2>`   | Standard Error (screen) |

#### tee Command
```bash
tee <file>              # Write to both screen and file (overwrites)
tee -a <file>           # Append to file instead of overwrite
tee file1 file2 file3   # Write to multiple files simultaneously

echo "text" | tee myfile           # Show on screen AND save to file
ls -l | tee file1 file2 file3      # Copy output to 3 files at once
```

**Difference from `>`:**
- `>` sends output ONLY to file (you don't see it on screen)
- `tee` sends output to BOTH screen and file at the same time

#### Pipes
```bash
command1 | command2     # Send output of command1 as input to command2

ls -ltr | more          # Page through long directory listing
ls -l | tail -1         # Show only the last line
```

#### File Display Commands
```bash
cat <file>              # Show entire file content at once
more <file>             # Page through file (spacebar=next, q=quit)
less <file>             # Page through file (scroll up/down, q=quit)
head <file>             # Show first 10 lines
tail <file>             # Show last 10 lines
tail -f <file>          # Follow file in real time (great for logs)
wc -c <file>            # Count characters/bytes
wc -l <file>            # Count lines
wc -w <file>            # Count words
```

---

### Module 5: Text Processing Commands (Mar 10 - Mar 11)

**Topics Covered:**
- `cut` — extract specific characters, bytes, or fields from text
- `awk` — powerful field-based text processing and pattern matching
- `grep` / `egrep` — search for patterns in files
- `sort` — sort lines in files
- `uniq` — filter duplicate lines
- `wc` — count lines, words, and characters

**Commands Mastered:**

#### cut — Extract Columns from Text
```bash
cut -c1 <file>           # Print only the 1st character of each line
cut -c1,3,5 <file>       # Print characters 1, 3, and 5
cut -c1-3 <file>         # Print characters 1 through 3 (a range)
cut -c1-3,6-8 <file>     # Print characters 1-3 and 6-8 (multiple ranges)
cut -b1-3 <file>         # Cut by bytes (same as -c for ASCII text)
cut -d: -f6 /etc/passwd  # Use : as delimiter, print field 6 (home directory)
```

**`-c` vs `-b` vs `-f`:**
- `-c` = cut by character position
- `-b` = cut by byte position (same as -c for standard ASCII)
- `-f` = cut by field (requires `-d` to set the delimiter)

**Real-world examples:**
```bash
cut -d: -f1 /etc/passwd  # Extract usernames only
cut -d: -f6 /etc/passwd  # Extract home directories only
ls -l | cut -c2-4        # Extract user permission chars (rwx) from ls
```

---

#### awk — Field-Based Text Processor
```bash
awk '{print $1}' <file>         # Print 1st word/field of each line
awk '{print $2}' <file>         # Print 2nd word/field
awk '{print $1,$3}' <file>      # Print fields 1 and 3 together
awk '{print $NF}' <file>        # Print LAST field of each line
awk '{print NF}' <file>         # Print NUMBER of fields per line

# Pattern matching
awk '/Linux/ {print}' <file>    # Print lines containing "Linux"
awk '/SSH/ {print}' <file>      # Print lines containing "SSH"

# Custom delimiter
awk -F: '{print $1}' /etc/passwd   # Use : as delimiter, print usernames
awk -F: '{print $6}' /etc/passwd   # Print home directories

# Modify a field on the fly
echo "hello tom" | awk '{$2="adam"; print $0}'       # → "hello adam"
cat file | awk '{$2="Sagar"; print $0}'              # Replace all 2nd words

# Conditional filtering
ls -l | awk '{ if ($9 == "Assh") print $0 }'         # Show only matching filename
awk 'length($0) > 30' <file>                         # Lines longer than 30 chars
```

**`$NF` vs `NF`:**
- `$NF` = the VALUE of the last field (the actual text)
- `NF` = the COUNT of how many fields are on that line

**awk vs cut:**
- `cut` is simpler — great for fixed character positions or delimited columns
- `awk` is more powerful — handles variable spacing, conditions, and calculations

---

#### grep / egrep — Search Patterns in Files
```bash
grep "pattern" <file>       # Search for pattern (case-sensitive)
grep -i "pattern" <file>    # Case-insensitive search
grep -c "pattern" <file>    # Count how many lines match
grep -n "pattern" <file>    # Show line numbers with matches
grep -v "pattern" <file>    # Invert — show lines that DON'T match
grep -vi "pattern" <file>   # Invert + case-insensitive

# Search in piped output
ls -l | grep Anything       # Find specific file in ls output
ls -l | grep -i anything    # Case-insensitive file search

# egrep = extended grep (supports | for multiple patterns)
egrep -i "Linux|SSH" <file>     # Match lines with "Linux" OR "SSH"
```

**Chaining grep with other tools:**
```bash
grep -vi Linux Anything | awk '{print $1}' | cut -c1-3
# → Lines without Linux → first word → first 3 chars
```

**grep flags quick reference:**

| Flag | What it does |
|------|-------------|
| `-i` | Case-insensitive |
| `-c` | Count matching lines |
| `-n` | Show line numbers |
| `-v` | Invert (show non-matching) |
| `-vi` | Invert + case-insensitive |

---

#### sort — Sort Lines
```bash
sort <file>              # Sort alphabetically (A-Z)
sort -r <file>           # Reverse sort (Z-A)
sort -k2 <file>          # Sort by the 2nd field/word
sort -k9 <file>          # Sort by 9th field (useful for ls -l output)

ls -l | sort             # Sort ls output alphabetically
ls -l | sort -k9         # Sort ls output by filename (column 9)
```

**Note:** `sort` does NOT modify the file — it only displays sorted output. To save: `sort file > sorted_file`

---

#### uniq — Remove Duplicate Lines
```bash
uniq <file>             # Remove consecutive duplicate lines
uniq -c <file>          # Show count of occurrences per line
uniq -d <file>          # Show only the DUPLICATE lines

# uniq only removes ADJACENT duplicates — always sort first!
sort <file> | uniq      # Sort then deduplicate (correct way)
sort <file> | uniq -c   # Sort, deduplicate, show counts
sort <file> | uniq -d   # Show only lines that appear more than once
```

**Key gotcha:** `uniq` only removes lines that are next to each other. Always use `sort | uniq` to catch all duplicates.

---

#### wc — Word Count
```bash
wc <file>               # Show lines, words, characters (all three)
wc -l <file>            # Count lines only
wc -w <file>            # Count words only
wc -c <file>            # Count characters/bytes

ls -l | wc -l           # Count number of items in directory
```

**Output format of `wc file`:**
`12  44  315  Anything` → 12 lines, 44 words, 315 characters

---

## 🎯 Key Concepts Learned

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

### Text Processing: When to Use What

| Tool | Best for |
|------|----------|
| `cut` | Fixed column positions or delimited fields |
| `awk` | Variable spacing, multiple fields, conditions |
| `grep` | Finding lines matching a pattern |
| `sort` | Ordering output alphabetically or by field |
| `uniq` | Removing duplicates (always sort first!) |
| `wc` | Counting lines, words, characters |

### Why Ownership Matters for Security
- Files in `/etc` are owned by root — regular users can't modify them
- A root-owned file in your own `/home` directory — you still can't delete it!

---

## 📝 Practice Exercises Completed

**Exercises 1–7:** Navigation, Links, Permissions, Ownership, ACL, Redirects, File Maintenance (Modules 3–4)

**Exercise 8: cut Practice**
```bash
cut -c1 Anything                  # First char of every line
cut -c1,3,5,7 Anything            # Specific characters
cut -c1-3 Anything                # Character range
cut -c1-3,6-8 Anything            # Multiple ranges
cut -d: -f6 /etc/passwd           # Field 6 (home dirs) from passwd
ls -l | cut -c2-4                 # Extract permission bits from ls
```

**Exercise 9: awk Practice**
```bash
awk '{print $1}' Anything                          # First word each line
awk '{print $1,$3}' Anything                       # Fields 1 and 3
awk '{print $NF}' Anything                         # Last word each line
awk '/Linux/ {print}' Anything                     # Lines with "Linux"
awk -F: '{print $1}' /etc/passwd                   # Usernames from passwd
awk -F: '{print $6}' /etc/passwd                   # Home dirs from passwd
echo "hello tom" | awk '{$2="adam"; print $0}'     # Replace 2nd word
cat Anything | awk '{$2="Sagar"; print $0}'        # Replace all 2nd words
awk 'length($0) > 30' Anything                     # Lines > 30 chars
ls -l | awk '{ if ($9 == "Assh") print $0 }'       # Conditional match
```

**Exercise 10: grep Practice**
```bash
grep Linux Anything                # Lines with "Linux"
grep -c Linux Anything             # Count = 3
grep -n Linux Anything             # With line numbers
grep -v Linux Anything             # Lines WITHOUT "Linux"
grep -vi Linux Anything            # Invert + case-insensitive
egrep -i "Linux|SSH" Anything      # Either pattern
grep -vi Linux Anything | awk '{print $1}' | cut -c1-3  # Chain all three!
```

**Exercise 11: sort & uniq Practice**
```bash
sort Anything                      # Alphabetical sort
sort -r Anything                   # Reverse sort
sort -k2 Anything                  # Sort by 2nd word
ls -l | sort -k9                   # Sort ls by filename
sort Anything | uniq               # Sort then deduplicate
sort Anything | uniq -c            # With occurrence counts
sort Anything | uniq -d            # Show only duplicates
```

**Exercise 12: wc Practice**
```bash
wc Anything                        # 12 lines, 44 words, 315 chars
wc -l Anything                     # Lines only
wc -w Anything                     # Words only
ls -l | wc -l                      # Count items in directory
```

---

## 🚀 What's Next

**Upcoming Modules:**
- [ ] Module 6: System Administration (processes, monitoring, logs)
- [ ] Module 7: Shell Scripting Basics

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
8. **Chain commands with pipes** — `grep | awk | cut` all in one line is powerful
9. **`sort` before `uniq`** — uniq only removes adjacent duplicates!
10. **`$NF` in awk** — always gets the last column, no matter how many fields

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
- `cut` = simple columns | `awk` = powerful processing | `grep` = pattern search
- Always `sort | uniq`, never just `uniq` on unsorted data
- Practice daily — consistency beats intensity!

---

---

### Module 5: System Administration (Mar 11-18, 2026) ✅ COMPLETE!

**Topics Covered:**
- User account management (useradd, usermod, userdel)
- sudo access and privileges
- Monitoring users and system activity
- System utility commands (date, uptime, hostname, uname)
- Process management (ps, top, kill)
- Scheduling tasks with crontab
- System monitoring (df, free, netstat)
- System logs (/var/log)
- Finding system information
- Environment variables

---

### User Account Management 👥

**Creating and Managing Users:**

```bash
# Create user (basic - no home directory)
useradd spiderman
id spiderman                # Verify user created
uid=1002(spiderman) gid=1002(spiderman)

# Delete user
userdel spiderman

# Create user WITH home directory
useradd -m spiderman
ls -ltr /home               # Verify home directory created
drwx------ 5 spiderman spiderman 4096 Mar 16 11:43 spiderman

# Create user with all options
useradd -g superheros -s /bin/bash -c "Ironman" -m -d /home/ironman ironman
# -g = primary group
# -s = shell
# -c = comment/description
# -m = create home directory
# -d = home directory path

# Set password
passwd ironman
# Enter: sagar12345 (example)

# Verify in system files
cat /etc/passwd | grep ironman
ironman:x:1003:1003:Ironman:/home/ironman:/bin/bash

cat /etc/shadow | grep ironman
ironman:!:20528:0:99999:7:::
```

**Managing Groups:**

```bash
# Create group
groupadd superheros

# Verify group created
grep superheros /etc/group
superheros:x:1003:

# Delete group
groupdel nonewgroup

# Add user to group
usermod -G superheros spiderman

# Verify user in group
grep spiderman /etc/group
superheros:x:1003:spiderman
spiderman:x:1002:

# Change group ownership of directory
chgrp -R superheros /home/spiderman
ls -ltr /home
drwx------ 5 spiderman superheros 4096 Mar 16 11:43 spiderman
```

**Key Files:**
- `/etc/passwd` - User account information
- `/etc/group` - Group information  
- `/etc/shadow` - Encrypted passwords

---

### sudo Access and Privileges 🔐

**Understanding su vs sudo:**

| Command | Password Required | Description |
|---------|------------------|-------------|
| `su - username` | Target user's password | Switch to another user |
| `su -` | Root password | Switch to root |
| `sudo command` | Your own password | Run command as root |
| `sudo -i` | Your own password | Get root shell |

**Practice Session:**

```bash
# Check current user
whoami
sagar

# Try switching to root (fails without root password)
su -
Password: 
su: Authentication failure

# Use sudo instead (works with your password)
sudo -i
[sudo] password for sagar:
# Now you're root!

# Add user to sudo group (Kali/Debian)
usermod -aG sudo sagar

# Verify sudo access
groups sagar
sagar : sagar sudo users

# Test sudo
sudo dmidecode
# Works! ✅
```

**Configuring sudo (Advanced):**

```bash
# Edit sudoers file (ALWAYS use visudo!)
sudo visudo

# Create wheel group (alternative sudo group)
groupadd wheel
usermod -aG wheel sagar

# Verify
grep wheel /etc/group
wheel:x:1005:sagar

# Switch to user and test
su - sagar
sudo dmidecode
# Works! ✅
```

**SSH Login Practice:**

```bash
# Create user
sudo -i
useradd -m pudi
passwd pudi
# Password: sagar12345

# Start SSH service
service ssh start

# Check IP
ifconfig
# IP: 172.24.58.219

# Login via SSH
ssh pudi@172.24.58.219
# First time: yes
# Password: sagar12345

# Verify login
whoami
pudi

pwd
/home/pudi

# Exit
exit
```

---

### Monitor Users 👀

**Who's Logged In:**

```bash
# Basic who command
who
sagar  pts/6  2026-03-17 12:35 (172.24.58.219)
sagar  pts/4  2026-03-17 11:59 (172.24.58.219)
sagar  pts/2  2026-03-17 11:57 (172.24.58.219)
sagar  pts/1  2026-03-17 11:07

# Detailed view with activity
w
13:12:07 up 2:05, 4 users, load average: 0.19, 0.05, 0.01
USER   TTY    FROM           LOGIN@  IDLE  JCPU  PCPU  WHAT
sagar  pts/6  172.24.58.219  12:35   1.00s 0.10s 0.01s w
sagar  pts/4  172.24.58.219  11:59   1.00s 0.31s 0.26s sudo -i

# Login history
last
sagar  pts/6  172.24.58.219  Tue Mar 17 12:35 - still logged in
pudi   pts/2  172.24.58.219  Tue Mar 17 11:53 - 11:57  (00:03)

# Get unique users
last | awk '{print $1}' | sort | uniq
pudi
sagar
wtmpdb

# User ID and groups
id
uid=1001(sagar) gid=1001(sagar) groups=1001(sagar),27(sudo),100(users)

id sagar
uid=1001(sagar) gid=1001(sagar) groups=1001(sagar),27(sudo),100(users)
```

---

### System Utility Commands 🛠️

```bash
# Current date and time
date
Tue Mar 18 13:30:45 IST 2026

# System uptime
uptime
13:30:45 up 2:23, 4 users, load average: 0.15, 0.08, 0.02

# Hostname
hostname
Sagar07

# System information (all)
uname -a
Linux Sagar07 6.6.87.2-microsoft-standard-WSL2 #1 SMP x86_64 GNU/Linux

# Kernel version
uname -r
6.6.87.2-microsoft-standard-WSL2

# Architecture
arch
x86_64

# Hardware info (requires root)
sudo dmidecode
# No SMBIOS nor DMI entry point found (WSL environment)
```

---

### Process Management ⚙️

**Viewing Processes:**

```bash
# Show YOUR processes only
ps
PID TTY      TIME CMD
896 pts/2    00:00:00 bash
926 pts/2    00:00:00 ps

# Show ALL processes
ps -e
PID TTY      TIME CMD
1 ?          00:00:00 systemd
2 ?          00:00:00 init
104 ?        00:00:00 cron
105 ?        00:00:00 dbus-daemon
...

# Show all with details (most useful!)
ps aux
USER    PID %CPU %MEM  VSZ  RSS TTY  STAT START TIME COMMAND
root      1  0.1  0.3 24440 13952 ?   Ss   11:54 0:00 /sbin/init
sagar   896  0.1  0.1  8420  5120 pts/2 Ss  12:06 0:00 -bash

# Show all in full format
ps -ef
UID   PID  PPID  C STIME TTY   TIME CMD
root    1     0  0 11:54 ?     00:00:00 /sbin/init
sagar 896   894  0 12:06 pts/2 00:00:00 -bash

# Show processes for specific user
ps -u sagar
PID TTY      TIME CMD
672 ?        00:00:00 systemd
896 pts/2    00:00:00 bash

# Find specific process
ps -ef | grep firewalld
# (no results - firewalld not running)
```

**top Command (Live Monitoring):**

```bash
# Start top
top
# Shows live CPU, memory, processes
# Press 'q' to quit

# Shortcuts inside top:
# c = show full command
# k = kill process
# m = sort by memory
# p = sort by CPU
# q = quit

# Show processes for specific user
top -u sagar
```

**kill Command:**

```bash
# List all signal types
kill -l
1) SIGHUP  2) SIGINT  3) SIGQUIT  9) SIGKILL  15) SIGTERM  ...

# Common signals:
# -15 (SIGTERM) = Gentle termination (default)
# -9 (SIGKILL) = Force kill (cannot be ignored)
# -2 (SIGINT) = Interrupt (like Ctrl+C)

# Example: Kill a sleep process
sleep 60 &
[1] 1640

ps -ef | grep sleep
sagar  1640  1605  0 17:05 pts/3  00:00:00 sleep 60

kill -9 1640
# Process terminated! ✅

# Alternative: killall (kill by name)
killall firefox
# Kills ALL firefox processes
```

---

### Crontab - Scheduled Tasks ⏰

**Cron Format:**

```
* * * * * command
│ │ │ │ │
│ │ │ │ └─── Day of week (0-7, Sunday = 0 or 7)
│ │ │ └───── Month (1-12)
│ │ └─────── Day of month (1-31)
│ └───────── Hour (0-23)
└─────────── Minute (0-59)
```

**Crontab Commands:**

```bash
# Edit cron jobs
crontab -e

# List cron jobs
crontab -l

# Remove all cron jobs
crontab -r

# Start cron service (WSL)
sudo service cron start

# Check if cron is running
ps aux | grep cron
root  104  0.0  0.0  4280  2304 ?  Ss  11:54  0:00 /usr/sbin/cron -f
```

**Example Cron Jobs:**

```bash
# Run every minute
* * * * * echo "hello sagar" >> /home/sagar/cron-test.txt

# Run at 6:30 PM daily
30 18 * * * echo "Evening task" >> /home/sagar/evening.txt

# Run every 2 minutes
*/2 * * * * date >> /home/sagar/time-log.txt

# Daily backup at 2 AM
0 2 * * * tar -czf /home/sagar/backup.tgz /home/sagar
```

**Verify Cron Works:**

```bash
# After setting up cron job, wait 1-2 minutes
cat /home/sagar/cron-test.txt
hello sagar
hello sagar
hello sagar
# It works! ✅

# Check cron logs
grep CRON /var/log/syslog
```

---

### System Monitoring 📊

**Disk Space (df):**

```bash
# Show disk usage (human-readable)
df -h
Filesystem   Size  Used Avail Use% Mounted on
/dev/sda1    100G   45G   50G  47% /

# Check specific directory
df -h /home
Filesystem   Size  Used Avail Use% Mounted on
/dev/sda1    100G   45G   50G  47% /
```

**Memory Usage (free):**

```bash
# Show RAM usage
free -h
              total   used   free  shared
Mem:          8.0G   3.2G   4.8G   200M
Swap:         2.0G   0B     2.0G

# Show in megabytes
free -m
              total   used   free  shared
Mem:          8192   3276   4916   204
Swap:         2048      0   2048
```

**Network Connections (netstat):**

```bash
# Show all listening ports with process names
netstat -tulpn
Proto Local Address  State      PID/Program
tcp   0.0.0.0:22     LISTEN     990/sshd
tcp   0.0.0.0:80     LISTEN     1234/nginx
```

**Other Monitoring:**

```bash
# I/O statistics
iostat

# System messages
dmesg | less

# CPU information
cat /proc/cpuinfo

# Memory information
cat /proc/meminfo
```

---

### System Logs 📋

**Important Log Directories:**

```bash
# Main log directory
cd /var/log

# List all logs
ls -l
total 1192
-rw-r--r-- 1 root root    669 Mar 18 16:58 alternatives.log
drwxr-x--- 2 root adm    4096 Feb 16 18:01 apache2
drwxr-xr-x 2 root root   4096 Mar 18 17:01 apt
-rw-rw---- 1 root utmp   4224 Mar 17 13:10 btmp
-rw-r--r-- 1 root root   9688 Mar 18 17:01 dpkg.log
-rw-rw-r-- 1 root utmp 293460 Mar 18 20:47 lastlog
-rw-rw-r-- 1 root utmp  31104 Mar 18 20:47 wtmp

# View logs with more
ll | more
```

**Key Log Files:**

| Log File | Purpose |
|----------|---------|
| `/var/log/syslog` | General system messages |
| `/var/log/auth.log` | Authentication attempts (sudo, SSH) |
| `/var/log/dpkg.log` | Package installations |
| `/var/log/apt/` | APT package manager logs |
| `/var/log/wtmp` | Login records (use `last`) |
| `/var/log/btmp` | Failed login attempts |

**Note:** Some logs like `boot.log`, `maillog`, `secure` are specific to Red Hat/CentOS. In Debian/Kali, use `journalctl` or check `/var/log/syslog` and `/var/log/auth.log` instead.

---

### Finding System Information 🔍

**System Release Info:**

```bash
# Kali/Debian version
cat /etc/os-release
PRETTY_NAME="Kali GNU/Linux Rolling"
NAME="Kali GNU/Linux"
ID=kali

# Red Hat version (not available in Kali)
cat /etc/redhat-release
# File not found

# Kernel info
uname -a
Linux Sagar07 6.6.87.2-microsoft-standard-WSL2 x86_64 GNU/Linux

# Architecture
arch
x86_64

# Hardware info (requires root)
sudo dmidecode
# dmidecode 3.6
# No SMBIOS nor DMI entry point found (WSL limitation)

# Hostname
hostname
Sagar07
```

---

### Environment Variables 🌍

**Common Environment Variables:**

```bash
# Show all environment variables
printenv
SHELL=/bin/bash
HOME=/home/sagar
USER=sagar
PATH=/usr/local/bin:/usr/bin:/bin
...

# Show specific variables
echo $SHELL
/bin/bash

echo $HOME
/home/sagar

echo $PATH
/usr/local/bin:/usr/bin:/bin:/usr/games

echo $USER
sagar

echo $PWD
/home/sagar
```

**Setting Environment Variables:**

```bash
# Temporary (current session only)
export TEST=1
echo $TEST
1

# Permanent (add to .bashrc)
vi ~/.bashrc
# Add at end:
export TEST=1

# Backup original first
cp .bashrc bashrc.orig

# Reload configuration
source ~/.bashrc

# Or logout and login again
exit
```

**Important Variables:**

| Variable | Purpose |
|----------|---------|
| `$HOME` | User's home directory |
| `$PATH` | Where system looks for commands |
| `$USER` | Current username |
| `$SHELL` | Default shell |
| `$PWD` | Current directory |
| `$MAIL` | Mail directory |

---

## 🎯 Module 5 Key Learnings

### Security Best Practices:
- ✅ Always use `sudo` instead of logging in as root
- ✅ Create users with `-m` flag to create home directories
- ✅ Use `passwd` immediately after creating users
- ✅ Monitor login attempts with `last` and `/var/log/auth.log`
- ✅ Schedule security scans with crontab
- ✅ Regular system monitoring with `df`, `free`, `netstat`

### Process Management:
- `ps aux` - View all processes with details
- `top` - Live process monitoring
- `kill -9 PID` - Force terminate process
- `ps -ef | grep name` - Find specific process

### Cron Gotchas:
- Service doesn't auto-start in WSL - must run `service cron start`
- Use `>>` to append, not `>` (overwrites)
- Always use absolute paths in cron jobs
- Check `/var/log/syslog` for cron execution

### Environment Variables:
- Temporary: `export VAR=value` (current session)
- Permanent: Add to `~/.bashrc` then `source ~/.bashrc`
- Never store passwords in environment variables!

---

## 📝 Practice Exercises Completed

**Exercise 1: User Management**
- Created users: spiderman, ironman, pudi
- Created group: superheros
- Added users to groups
- Set passwords
- SSH login practice

**Exercise 2: sudo Configuration**
- Added user to sudo group
- Created wheel group
- Tested sudo access
- Verified with `groups` command

**Exercise 3: Process Management**
- Viewed processes with `ps aux`
- Monitored with `top`
- Killed processes with `kill -9`
- Found processes with `grep`

**Exercise 4: Crontab**
- Created scheduled tasks
- Tested with simple echo commands
- Verified execution
- Checked logs

**Exercise 5: System Monitoring**
- Checked disk with `df -h`
- Monitored memory with `free -h`
- Viewed logs in `/var/log`

**Exercise 6: Environment Variables**
- Set TEST variable
- Added to `.bashrc`
- Tested persistence

---

## 🚀 What's Next

**Remaining Modules:**
- [x] Module 3: System Access and File System ✅
- [x] Module 4: Linux Fundamentals ✅
- [x] Module 5: System Administration ✅
- [ ] Module 6: Shell Scripting Basics (Next!)
- [ ] Module 7: SSH + Networking Commands (2 videos only)

**Target:** Complete Linux by March 20, 2026  
**Then:** Python basics starting March 21! 🐍

---

**Last Updated:** March 18, 2026  
**Status:** Module 5 COMPLETE! 95% done with entire Linux course! 🎉
