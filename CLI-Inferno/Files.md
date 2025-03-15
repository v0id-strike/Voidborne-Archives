## **📌 Phase 1: Navigating the Linux Filesystem**  

Navigation in Linux is as fundamental as using a mouse in Windows. It allows us to move across the system, work with directories and files, and retrieve information efficiently. Mastering navigation enables us to manage files, search for them, and use advanced options to customize outputs.  

### **1️⃣ Where Are We? (`pwd`)**  
Before navigating, we need to determine our current location. The `pwd` (print working directory) command does this:  
```bash
pwd
```
This output shows that we are inside the `/home/user` directory.  

### **2️⃣ Listing Directory Contents (`ls`)**  
To see the contents of a directory, use `ls`:  
```bash
ls
```
By default, `ls` only lists directories and files. To get more details, use:  
```bash
ls -l    # Long format (permissions, size, owner, etc.)
ls -a    # Show hidden files (files starting with ".")
ls -la   # Combine both
ls -lh   # Human-readable file sizes (e.g., KB, MB, GB)
ls -lt   # Sort by modification time
ls -S    # Sort by file size (largest first)
```
Example output of `ls -l`:  
```bash
total 32
drwxr-xr-x 2 user user_group 4096 Nov 13 17:37 Desktop
drwxr-xr-x 3 user user_group 4096 Nov 15 03:26 Downloads
-rw-r--r-- 1 user user_group 2048 Nov 10 12:15 notes.txt
```

#### **Understanding the Output**  
| Column         | Description                                  |
| -------------- | -------------------------------------------- |
| `drwxr-xr-x`   | Type & permissions (d = directory, - = file) |
| `2`            | Number of hard links to the file/directory   |
| `user`         | Owner of the file/directory                  |
| `user_group`   | Group owner                                  |
| `4096`         | File size in bytes (4 KB)                    |
| `Nov 13 17:37` | Last modification date/time                  |
| `Desktop`      | File/directory name                          |

To see all contents, including hidden files (`.` prefix), use:  
```bash
ls -la
```

### **3️⃣ Navigating the Filesystem (`cd`)**  
To move between directories, use `cd` (change directory):  
```bash
cd /usr/share    # Go directly to /usr/share
cd -           # Switch to the previous directory
cd ~           # Go to home directory
cd ..          # Move one level up (parent directory)
cd ../..       # Move two levels up
cd /           # Go to root directory
```
💡 **Tip:** Use `TAB` for **autocompletion**. Type `cd /usr/s` then press `[TAB]` twice to list all directories starting with `s`.  

### **4️⃣ Listing Other Directories (`ls [path]`)**  
Instead of moving into a directory, we can list its contents directly:  
```bash
ls -l /var/
```
Example output:  
```bash
drwxr-xr-x  2 root root     4096 May 15 18:54 backups
drwxr-xr-x 18 root root     4096 Nov 15 16:55 cache
drwxrwsrwt  2 root whoopsie 4096 Jul 25  2018 crash
```

---
## **📌 Phase 2: Working with Files and Directories**  

One of the biggest differences between Linux and Windows is how files are accessed and managed. In Windows, most users rely on graphical tools like Explorer, while in Linux, the **terminal** provides a powerful alternative. Working with files via commands is often faster, more efficient, and allows for advanced operations such as **batch editing, automation, and regex-based modifications**.  

### **5️⃣ Creating Files and Directories**  
Creating an Empty File (`touch`):  
```bash
touch info.txt
```
Creating a Directory (`mkdir`):
```bash
mkdir Storage
```  
Instead of creating each directory one by one, use the `-p` (parents) option to create multiple directories at once:  
```bash
mkdir -p Storage/local/user/documents
```
To visualize the directory structure, use:  
```bash
tree .
```
📌 **Example Output:**  
```
.
├── info.txt
└── Storage
    └── local
        └── user
            └── documents

4 directories, 1 file
```

You can create files directly in a specific directory by specifying its path:  
```bash
void@machine[machine]$ touch ./Storage/local/user/userinfo.txt
```
📌 **Updated Directory Structure:**  
```
.
├── info.txt
└── Storage
    └── local
        └── user
            ├── documents
            └── userinfo.txt

4 directories, 2 files
```

### **6️⃣ Moving and Renaming Files (`mv`)**  
The `mv` command allows both **renaming** and **moving** files.  
To rename `info.txt` to `information.txt`: 
```bash
mv info.txt information.txt
```
Create a new file `readme.txt` and move both `information.txt` and `readme.txt` to `Storage/`:
```bash
touch readme.txt
mv information.txt readme.txt Storage/
```
📌 **Updated Directory Structure:**  
```
.
└── Storage
    ├── information.txt
    ├── local
    │   └── user
    │       ├── documents
    │       └── userinfo.txt
    └── readme.txt

4 directories, 3 files
```

### **7️⃣ Copying Files (`cp`)**  
If you need to **copy** rather than move files, use `cp`.  
Copy `readme.txt` into `Storage/local/`:  
```bash
cp Storage/readme.txt Storage/local/
```
📌 **Updated Directory Structure:**  
```
.
└── Storage
    ├── information.txt
    ├── local
    │   ├── readme.txt
    │   └── user
    │       ├── documents
    │       └── userinfo.txt
    └── readme.txt

4 directories, 4 files
```

---

## **📌 Phase 3: Finding Files and Directories**

When working with a Linux system, efficiently locating files and directories is crucial. Instead of manually browsing through folders, we can use various command-line tools to find configuration files, user scripts, logs, and other essential files. These tools streamline the search process and help filter results based on specific attributes.

### 8️⃣ The `which` Command
The `which` command helps locate executable files by returning the path of a program that would be executed when called. This is useful for checking if certain utilities (like `curl`, `wget`, `netcat`, `python`, `gcc`) are available.
```bash
which python
```
If the program does not exist, no output is displayed.

### 9️⃣ The `find` Command
The `find` command is a powerful tool that searches for files and directories based on various criteria such as name, type, size, modification date, and ownership.
Syntax:
```bash
find <location> <options>
```
Example:
Search for all `.conf` files owned by `root`, larger than 20 KB, and modified after March 3, 2020:
```bash
find / -type f -name "*.conf" -user root -size +20k -newermt 2020-03-03 -exec ls -al {} \; 2>/dev/null
```

Breakdown of Options:

| Option                | Description                                        |
| --------------------- | -------------------------------------------------- |
| `-type f`             | Searches for files (`d` for directories).          |
| `-name "*.conf"`      | Finds files matching the `.conf` extension.        |
| `-user root`          | Filters results to files owned by the `root` user. |
| `-size +20k`          | Searches for files larger than 20 KiB.             |
| `-newermt 2020-03-03` | Finds files modified after the given date.         |
| `-exec ls -al {} \;`  | Executes `ls -al` on each result.                  |
| `2>/dev/null`         | Suppresses error messages.                         |

Practical Use Cases:
- Find SSH keys:
  ```bash
  find /home -type f -name "id_rsa*"
  ```
- Locate web server logs modified in the last 7 days:
  ```bash
  find /var/log -type f -name "*.log" -mtime -7
  ```
- Search for hidden files:
  ```bash
  find /home -type f -name ".*"
  ```

### 🔟 The `locate` Command
The `locate` command offers a faster way to search for files by querying a pre-built database instead of scanning the entire file system.
Update the Database:
```bash
sudo updatedb
```
Find all `.conf` files:
```bash
locate "*.conf"
```
To refine search results, pipe `locate` output into `grep`:
```bash
locate "*.conf" | grep network
```

### Comparing `which`, `find`, and `locate`
| Command  | Use Case                        | Pros                | Cons                              |
| -------- | ------------------------------- | ------------------- | --------------------------------- |
| `which`  | Locate binary paths             | Fast                | Only works for executables        |
| `find`   | Search files by attributes      | Highly customizable | Can be slow on large file systems |
| `locate` | Search by name using a database | Very fast           | Requires `updatedb` to be current |

---

## **📌 Phase 4: File Descriptors and Redirections**

A **file descriptor (FD)** is a number assigned by the Linux system to track open files, sockets, or other I/O resources. The operating system uses these numbers to manage input and output operations.

By default, Linux assigns three standard file descriptors:

- **STDIN (0)** – Standard Input (keyboard or file input)
- **STDOUT (1)** – Standard Output (normal program output)
- **STDERR (2)** – Standard Error (error messages)

For example, when using the `cat` command, text entered as **STDIN** (FD 0) is immediately displayed as **STDOUT** (FD 1):

```bash
void@machine[~]$ cat
Some Input      # (User types this)
Some Input      # (Output appears)
```

### **1️⃣1️⃣ Redirection**

Redirection allows us to control where input and output go.

Some commands produce errors. If we only want successful results and hide errors, we can redirect **STDERR (FD 2)** to `/dev/null`, a special file that discards data.
```bash
find /etc/ -name shadow 2>/dev/null
```
Now, only valid results appear, and "Permission denied" messages are hidden.

To save output to a file instead of displaying it on the screen, we redirect **STDOUT (FD 1)** using `>`:
```bash
find /etc/ -name shadow > results.txt
```
Now, the file `results.txt` contains the output.

We can store **STDOUT** and **STDERR** in different files:
```bash
find /etc/ -name shadow 1> output.txt 2> errors.txt
```
- `output.txt` will contain successful results.
- `errors.txt` will contain error messages.

Instead of typing input manually, we can provide input from a file using `<`:
```bash
cat < output.txt
```
This makes `cat` read from `output.txt` instead of waiting for manual input.

If we use `>`, it replaces the file’s content. To **append** data instead, use `>>`:
```bash
find /etc/ -name passwd >> output.txt 2>/dev/null
```
Now, new results are added to `output.txt` without deleting existing data.

We can provide multiple lines of input using `<<` and EOF:
```bash
cat << EOF > stream.txt
Hack The Box
EOF
```
This saves "Hack The Box" in `stream.txt`.

### **1️⃣2️⃣ Using Pipes (|) to Process Output**
Pipes (`|`) allow us to send output from one command to another.

If we want only lines containing "systemd", we can use `grep`:
```bash
find /etc/ -name "*.conf" 2>/dev/null | grep systemd
```
This filters the output and only shows files related to "systemd".

We can count how many lines were found using `wc -l`:
```bash
find /etc/ -name "*.conf" 2>/dev/null | grep systemd | wc -l
```
Now, only the **number** of matching files is displayed.

---

## **📌 Phase 5: Filter Contents**

### **1️⃣3️⃣ More ways to see file content**
The `more` command displays file content one screen at a time. Press `[Space]` to go forward and `[Q]` to exit.
```bash
cat /etc/passwd | more
```
Output remains visible in the terminal after exiting.

Similar to `more`, but with additional navigation features.
```bash
less /etc/passwd
```
Unlike `more`, the output disappears from the terminal after exiting.

Shows the first 10 lines of a file (default).
```bash
head /etc/passwd
```
Shows the last 10 lines.
```bash
tail /etc/passwd
```

### **1️⃣4️⃣ Content filtering**
Sorts the lines alphabetically or numerically.
```bash
cat /etc/passwd | sort
```

Searches for specific patterns in a file.
```bash
cat /etc/passwd | grep "/bin/bash"
```
To exclude matches, use `-v`:
```bash
cat /etc/passwd | grep -v "nologin"
```

Extracts specific columns from text using delimiters.
```bash
cat /etc/passwd | cut -d":" -f1
```

Replaces characters.
```bash
cat /etc/passwd | tr ":" " "
```

Formats text into a table.
```bash
cat /etc/passwd | tr ":" " " | column -t
```

Prints specific columns.
```bash
cat /etc/passwd | awk '{print $1, $NF}'
```

Finds and replaces text.
```bash
cat /etc/passwd | sed 's/bin/HTB/g'
```

Counts lines in output.
```bash
cat /etc/passwd | wc -l
```

 ---

## **📌 Phase 6: Permission Management**
# Linux Permissions: A Simplified Guide

### **1️⃣5️⃣  Understanding Linux Permissions**

Linux permissions control access to files and directories. Each file or directory has:
- **Owner** (user who created it)
- **Group** (assigned team of users)
- **Others** (everyone else)

Permissions are like keys, granting access based on three levels:
1. **Read (r)** – View file contents or list directory contents.
2. **Write (w)** – Modify file contents or create/delete files in a directory.
3. **Execute (x)** – Run files as programs or access directories.

### **1️⃣6️⃣ Checking File Permissions**

Use `ls -l` to view permissions:
```bash
ls -l
-rwxr-xr-- 1 user group 1641 May 4 23:42 example.txt
```

**Breakdown:**
- `-` (File type: `-` for file, `d` for directory, `l` for link)
- `rwx` (Owner permissions: Read, Write, Execute)
- `r-x` (Group permissions: Read, Execute)
- `r--` (Others: Read-only)
- `user` (Owner of the file)
- `group` (Assigned user group)

### **1️⃣7️⃣ Directory Permissions**

- To **enter a directory**, you need **execute (x)** permission.
- To **list contents**, you need **read (r)** permission.
- To **create/delete files**, you need **write (w)** permission.

Example error when lacking execute permission:
```bash
ls: cannot access 'mydirectory/script.sh': Permission denied
```

### **1️⃣8️⃣ Modifying Permissions**

Use the `chmod` command:
- Add permission: `chmod u+x file` (Give owner execute permission)
- Remove permission: `chmod g-w file` (Remove write permission from group)
- Set exact permissions using octal notation:
    - `chmod 754 file`
    - **7** (Owner: Read, Write, Execute)
    - **5** (Group: Read, Execute)
    - **4** (Others: Read-only)

#### Octal Permission Table:

| Octal | Binary | Meaning                    |
| ----- | ------ | -------------------------- |
| 7     | 111    | rwx (Read, Write, Execute) |
| 6     | 110    | rw- (Read, Write)          |
| 5     | 101    | r-x (Read, Execute)        |
| 4     | 100    | r-- (Read-only)            |

### **1️⃣9️⃣ Changing Ownership**

Use `chown` to change owner and group:
```bash
chown newuser:newgroup file
```

Example:
```bash
chown root:root shell
-rwxr-xr-- 1 root root 0 May 4 22:12 shell
```

### **2️⃣0️⃣ Special Permissions**

#### **SUID (Set User ID)**
- Files with **SUID** run as the file owner, not the executing user.
- Example:
    - `chmod u+s file` (Sets SUID bit)
    - Appears as `rws` in permissions.
- Risk: Can grant unintended root access if misused.

#### **SGID (Set Group ID)**
- When set on a **file**, it runs with the group’s permissions.
- When set on a **directory**, new files inherit the group.
- Example:
    - `chmod g+s directory`
    - Appears as `rwxr-sr-x`

#### **Sticky Bit**
- Used on shared directories to **prevent deletion** by non-owners.
- Example:
    - `chmod +t directory`
    - Appears as `drwxrwxr-t`

Example:
```bash
drwxrwxr-t 3 user group 4096 Jan 12 12:30 shared_folder
```
- **Lowercase `t`**: Execute permission is set.
- **Uppercase `T`**: Execute permission is missing.
