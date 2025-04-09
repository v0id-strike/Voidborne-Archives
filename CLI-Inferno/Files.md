### 1️⃣ **Core Navigation Commands**  
| Command | Description                   | Example                 |
| ------- | ----------------------------- | ----------------------- |
| `pwd`   | Show current directory        | `pwd` → `/home/user`    |
| `ls`    | List contents                 | `ls -la` (hidden files) |
| `cd`    | Change directory              | `cd /var/log`           |
| `tree`  | Visualize directory structure | `tree -L 2`             |

**Pro Tip:**  
```bash
cd -  # Switch to previous directory
```

---

### 2️⃣ **File Operations**  
| Task        | Command    | Example                       |
| ----------- | ---------- | ----------------------------- |
| Create file | `touch`    | `touch notes.txt`             |
| Create dir  | `mkdir -p` | `mkdir -p project/{src,docs}` |
| Move/Rename | `mv`       | `mv old.txt new.txt`          |
| Copy        | `cp -r`    | `cp -r dir1/ dir2/`           |
| Delete      | `rm -rf`   | `rm -rf temp/`                |

**Warning:**  
❌ `rm -rf /` → **Destructive!** Always double-check paths.

---

### 3️⃣ **Finding Files**  
| Tool     | Use Case             | Example                           |
| -------- | -------------------- | --------------------------------- |
| `find`   | Advanced searches    | `find / -name "*.conf" -size +1M` |
| `locate` | Fast filename search | `locate passwd`                   |
| `which`  | Find executables     | `which python`                    |

**Key `find` Options:**  
```bash
find /var/log -type f -mtime -7 -exec ls -lh {} \;
```
- `-type f`: Files only  
- `-mtime -7`: Modified in last 7 days  
- `-exec`: Run command on results  

---

### 4️⃣ **File Contents & Filtering**  
| Command       | Function          | Example                               |
| ------------- | ----------------- | ------------------------------------- |
| `cat`         | Display file      | `cat /etc/passwd`                     |
| `grep`        | Search text       | `grep "root" /etc/passwd`             |
| `head`/`tail` | View start/end    | `tail -n 20 log.txt`                  |
| `awk`         | Column extraction | `awk -F: '{print $1,$6}' /etc/passwd` |
| `sed`         | Text replacement  | `sed 's/foo/bar/g' file.txt`          |

**Pipeline Magic:**  
```bash
cat logs.txt | grep "ERROR" | awk '{print $2}' | sort | uniq -c
```

---

### 5️⃣ **Permissions Deep Dive**  
#### Permission Types:
| Symbol | File           | Directory           |
| ------ | -------------- | ------------------- |
| `r`    | Read content   | List files          |
| `w`    | Modify content | Create/delete files |
| `x`    | Execute script | Enter directory     |

#### Octal Notation:
| #   | Permission               |
| --- | ------------------------ |
| 7   | rwx (Read+Write+Execute) |
| 6   | rw- (Read+Write)         |
| 5   | r-x (Read+Execute)       |

**Critical Commands:**  
```bash
chmod 750 script.sh  # Owner:rwx, Group:r-x, Others:--- 
chown user:group file
```

#### Special Permissions:
| Bit        | Effect            | Example                      |
| ---------- | ----------------- | ---------------------------- |
| SUID (4)   | Run as owner      | `chmod 4755 /usr/bin/passwd` |
| SGID (2)   | Inherit group     | `chmod 2770 /shared`         |
| Sticky (1) | Restrict deletion | `chmod 1777 /tmp`            |

---

### 6️⃣ **Redirection & Pipes**  
| Symbol | Function        | Example                   |
| ------ | --------------- | ------------------------- |
| `>`    | Overwrite file  | `ls > output.txt`         |
| `>>`   | Append to file  | `echo "new" >> log.txt`   |
| `2>`   | Redirect errors | `cmd 2> errors.log`       |
| `\|`   | Pipe output     | `cat file \| grep "text"` |

**Advanced Redirection:**  
```bash
command > >(tee stdout.log) 2> >(tee stderr.log >&2)
```

---

### 7️⃣ **Exercises**  
1. **Navigation:**  
   - List all `.conf` files in `/etc` sorted by size (`ls -lS /etc/*.conf`)  
   - Create directory tree `backups/{monthly,weekly}/2023`  

2. **Permissions:**  
   - Find all SUID binaries:  
     ```bash
     find / -perm -4000 2>/dev/null
     ```  
   - Change `/shared` to:  
     - Group ownership: `developers`  
     - Permissions: `rwxrwx---` (770)  

3. **Filtering:**  
   - Extract usernames and shells from `/etc/passwd`:  
     ```bash
     awk -F: '{print $1,$7}' /etc/passwd | column -t
     ```  

---

### 8️⃣ **Pro Tips**  
- **Secure file copies**: Use `rsync -avz` for large transfers.  
- **Permission calculator**:  
  ```bash
  stat -c "%a %n" *  # Show octal perms for all files
  ```  
- **Quick archive**:  
  ```bash
  tar -czvf backup.tar.gz /path/to/files
  ```  

---

### 9️⃣ **Visual Cheatsheet**  
```
# Permission Breakdown
-rwxr-xr--  1 user group  size date filename
│└─┬─┘└─┬─┘
│ │  │   └── Others: r--
│ │  └────── Group: r-x
│ └───────── Owner: rwx
└─────────── File type (-,d,l)
```
