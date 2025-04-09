
## **1️⃣ Manual Pages (`man`)**
Linux's built-in documentation system accessible via the `man` command.

### **Key Features**
- **Structured sections** (1-9) for different command types
- **Quick reference** for commands, config files, and system calls
- **Ubiquitous** - available offline on all Linux systems

### **Usage**
```bash
man [section] command
```

### **Examples**
```bash
man ls           # Standard command documentation
man 5 passwd     # Documentation for /etc/passwd file format
man 3 printf     # C library function documentation
```

### **Navigation in man pages**
| Key        | Action          |
| ---------- | --------------- |
| `Space`    | Next page       |
| `Enter`    | Next line       |
| `/pattern` | Search forward  |
| `?pattern` | Search backward |
| `n`        | Next match      |
| `q`        | Quit            |

### **Finding Relevant man Pages**
```bash
man -k "network"          # Search all man pages
man -f passwd             # Show all sections for 'passwd'
whatis ls                 # Brief description of command
```

## **2️⃣ Info Pages (`info`)**
More detailed documentation system, often with hyperlinked content.

### **Key Features**
- **Hierarchical documentation** with nodes
- **More detailed** than man pages for complex tools
- **Hyperlinked navigation** between related topics

### **Usage**
```bash
info command
```

### **Navigation in info**
| Key     | Action            |
| ------- | ----------------- |
| `n`     | Next node         |
| `p`     | Previous node     |
| `u`     | Up one level      |
| `Enter` | Follow link       |
| `Tab`   | Jump to next link |
| `q`     | Quit              |

### **Examples**
```bash
info coreutils            # Documentation for GNU core utilities
info emacs                # Comprehensive Emacs manual
info bash                 # Full Bash manual
```

## **3️⃣ Online Documentation**
### **System Documentation**
```bash
/usr/share/doc/           # Location of package documentation
less /usr/share/doc/package/README
```

### **Command Help Options**
```bash
command --help            # Brief usage (GNU style)
command -h                # Brief usage (BSD style)
```

### **Package Documentation**
```bash
dpkg -L package | grep doc  # Find docs for Debian packages
rpm -qd package           # List docs for RPM packages
```

## **4️⃣ Comparison: man vs info**

| Feature        | man Pages | info Pages       |
| -------------- | --------- | ---------------- |
| Detail Level   | Concise   | Comprehensive    |
| Navigation     | Linear    | Hyperlinked      |
| Availability   | Universal | Mostly GNU tools |
| Learning Curve | Easier    | Steeper          |
| Examples       | Few       | Many             |

## **5️⃣ Documentation Best Practices**
1. **Start with `--help`** for quick reference
2. **Use `man`** for standard command syntax
3. **Consult `info`** for in-depth GNU tool documentation
4. **Check `/usr/share/doc`** for package-specific docs
5. **Search online** for tutorials and community knowledge

## **6️⃣ Finding Documentation**
### **For Installed Commands**
```bash
type command              # Identify command source
command --version         # Check version
```

### **For System Components**
```bash
man hier                  # Filesystem hierarchy documentation
man 7 glob                # Filename pattern matching
man 7 signal              # Linux signals reference
```

## **7️⃣ Advanced Tips**
- **Search all man pages**: `man -K "keyword"`
- **Print man page as PDF**: `man -t bash | ps2pdf - bash.pdf`
- **View compressed docs**: `zless /usr/share/doc/package/README.gz`
- **Create custom man pages**: Store in `~/man/man1/`

## **8️⃣ Recommended Online Resources**
1. **Linux man pages online**: [man7.org](https://man7.org/linux/man-pages/)
2. **GNU documentation**: [www.gnu.org/manual](https://www.gnu.org/manual/)
3. **TLDR pages**: [tldr.sh](https://tldr.sh/) (Simplified man pages)
4. **Arch Linux Wiki**: [wiki.archlinux.org](https://wiki.archlinux.org/)
5. **Stack Overflow**: [stackoverflow.com](https://stackoverflow.com/)

Remember: The ability to quickly find and understand documentation is one of the most valuable skills for any Linux user or administrator!
