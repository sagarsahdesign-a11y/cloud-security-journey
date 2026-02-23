# Linux Learning Progress

## Week 1 (Feb 17-23, 2026)

### Day 1 - Feb 19
**Labs Completed:**
- Getting Started with Linux
- Basic File Operations
- Delete and Move Files
- Linux User Group and File Permissions

**Commands Learned:**
```bash
# Navigation
pwd                    # Print working directory
ls                     # List files
ls -la                 # List all files (detailed)
cd folder              # Change directory
cd ..                  # Go up one level
mkdir folder           # Create directory

# File Operations
touch file.txt         # Create empty file
cat file.txt           # Show file contents
echo "text" > file     # Write to file
rm file.txt            # Remove file
cp source dest         # Copy file
cp -r folder dest      # Copy directory
mv source dest         # Move/rename file

# User Management
whoami                 # Show current user
sudo groupadd name     # Create group
sudo adduser user      # Create user (interactive)
sudo useradd -m -g group user  # Create user with group
id username            # Show user info
ls /home               # List all users
```

---

### Day 2 - Feb 21
**Lab Completed:**
- File and Directory Operations

**Commands Practiced:**
```bash
# Creating
touch file1.txt
echo "Hello" > file2.txt
mkdir testdir

# Listing
ls                     # Basic list
ls -l                  # Detailed list
ls -a                  # Show hidden files
ls -la                 # All files, detailed
ls -R                  # Recursive list

# Copying
cp file.txt copy.txt
cp file.txt folder/
cp -r folder folder_copy

# Moving/Renaming
mv old.txt new.txt
mv file.txt folder/

# Removing
rm file.txt            # Remove file
rm -i file.txt         # Ask before removing
rmdir empty_folder     # Remove empty directory
rm -r folder           # Remove directory recursively
rm -rf folder          # Force remove (DANGEROUS!)

# Hidden Files
.filename              # Files starting with . are hidden
ls -a                  # Show hidden files
```

**Key Notes:**
- Absolute path: `/home/user/file` (starts with `/`)
- Relative path: `folder/file` (no leading `/`)
- `cp` = copy (original stays)
- `mv` = move (original disappears)
- `rm` = permanent deletion (no undo!)
- Hidden files start with `.`
