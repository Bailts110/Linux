[[1- Intro to Linux]]
[[0-History of Linux]]
#Shell #Linux #FileSystem_Linux #Linux_Concepts

> [!note]+ ALL Linux Commands Are Case Sensitive

## 📁 Directory Navigation

```bash
ls        # List files and directories in current folder
ls -a     # Include hidden files (those starting with .)
ls -F     # Append indicator (e.g., / for directories)
ls -alf   
# Combine options: show all, long listing, and file type
ls -lh # -l for more Detials -h for dishplay size in human Reading ...
ls -ld # -d display the Directory without its Content
ls -R # Show the Content of Dircetory
ls -i # to show Inode 
ls -l ori* *link #  to get all File | Folder that
# start Name with orgi or end with *link* ::Good For searching::
sudo tree # Best than (Ls -R) display the entire Directory Content with Human Readable way 
pwd       # Print current working directory
```

> [!tip]+ Combine `ls` options to get more useful listings.

---

## ⚙️ Shell Commands vs Shell Builtins
[[3- Linux Stream]]

- **Executable Shell Commands**: Separate files stored in `/bin`, `/usr/bin`, etc.
    
    - Example: `pwd`
        
    - Check with: `which pwd`
        
    
    ![[Pasted image 20250606111205.png]]
    
- **Shell Builtins**: Part of the shell program itself.
    
    - Example: `cd`, `echo`
        
    - Check with: `type cd`
        
    
    ![[Pasted image 20250606110858.png]]
    

---

## 🧹 File Operations
[[5- File Management]]

```bash
rm <file>       # Remove a file
rmdir <dir>     # Remove an empty directory
rm -r <dir>     # Remove a directory and its contents recursively
sudo <command>  # Run command with elevated privileges
```

### 📖 Help & Documentation

```bash
man <command>   # Open manual page (e.g., man ls)
which <cmd>     # Show full path of an executable
```

---

## ✍️ Editing with `vi`

> [!note]+ `vi` is a universal text editor available on all Linux systems.

### Modes in `vi`:

- **Command Mode** (default): navigate, delete, copy, etc.
    
- **Insert Mode**: press `i` to enter, `Esc` to leave
    

### Common Commands

```vi
:w      # Save file
:q      # Quit
:q!     # Quit without saving
:.!ls   # Run shell command and insert output
```

> [!info]+ Navigation uses `h`, `j`, `k`, `l` as arrow keys since vi predates arrow keys.

---

## 📜 The Unix Philosophy

1. **Small is Beautiful**
    
2. **Do One Thing Well**
    
3. **Prototype Early**
    
4. **Favor Portability**
    
5. **Use Flat Text Files**
    

> [!note]+ Everything in Linux is a file:

- Regular files: `file.txt`
    
- Directories: special files that list other files
    
- Devices: `/dev/sda`, `/dev/tty`
    
- System info: `/proc/cpuinfo`, `/sys`
    
- Pipes & sockets
    
- Symlinks
    

---

## 💻 Terminal Architecture

> [!note]+ Terminal (hardware or emulator) ⟶ Shell (like bash) ⟶ Kernel ⟶ Hardware

- `TTY`: terminal sessions (e.g., `/dev/pts/0`)
    
- Switch TTYs: `Ctrl + Alt + F3`
    
- Check active TTYs with `ps`
    

---

## 🔐 SSH (Secure Shell)

```bash
sudo apt install openssh-server   # If not installed
ssh username@localhost            # Connect to your machine
```

- Disconnect: type `exit`
    
- See shells: `ls /bin/*sh`
    
- Current shell: `echo $0`
    

---

## 🪄 Shell Expansions

### File Globbing

```bash
touch ff{2..6}    # Expands to ff2 ff3 ff4 ff5 ff6
ls file[1-4]      # Matches file1 to file4
ls file[!2]       # Not file2
ls file?          # Any single char after file
```

> [!note]+ Expansion is done by the shell, not the terminal.

### Variables

```bash
var1=10
echo $var1
export var1      # Make it global to subshells
```

- `${var-unset}`: default value if unset
    
- Multiple commands: `echo $var; ls`
    

### Search Variables

```bash
set | grep var
```

---

## 🔍 Autocomplete

```bash
compgen -v   # List all variables
```

---

## 🧾 Declare & Math

```bash
declare -i n1=5 n2=6  # Integer variables
echo $((n1 * n2))
```

### Math with `expr`

```bash
expr 5 + 2
```

> [!tip]+ Use `bc` for floating-point math:

```bash
echo "3.5 / 2" | bc
```

![[Screenshot from 2025-06-07 03-51-55.png]]  
![[Screenshot from 2025-06-07 03-57-04.png]]

---

## 🔐 Login vs Non-login Shells

```bash
echo $0    # If starts with '-', it's a login shell
```

| Login Shell          | Non-Login Shell        |
| -------------------- | ---------------------- |
| Needs login          | Opened by terminal GUI |
| Loads `/etc/profile` | Loads `.bashrc`        |

> [!important]+ Place permanent env variables in:

- `/etc/profile` (for all users)
    
- `~/.bashrc` (for current user)
    

---



- Add [[Aliases]] and backlinks for key commands like `[[ls]]`, `[[grep]]`, `[[vi]]`
    
- Use tags like `#linux`, `#shell`, `#terminal`, `#ssh`
    
- Split large sections into separate notes and use `[[shell-expansions]]`, `[[vi-editor]]`, etc.
    
- Create a **Command Reference Table** with shortcuts and meanings
    
- Use the **Obsidian Graph View** to visually connect concepts
    

> [!idea]+ Consider creating a **Linux Cheatsheet Canvas** in Obsidian using Canvas view for visual learners.