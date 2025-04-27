
# 📝 Mastering Background Processes & Debugging

### 1️⃣ **Process Management Essentials**  
#### Key Commands:
| Command      | Description                       | Example                |
| ------------ | --------------------------------- | ---------------------- |
| `ps`         | Snapshot of processes             | `ps aux \| grep nginx` |
| `top`/`htop` | Interactive process viewer        | `htop -u www-data`     |
| `jobs`       | List background jobs              | `jobs -l`              |
| `bg`/`fg`    | Move job to background/foreground | `bg %1`                |
| `nohup`      | Run process immune to hangups     | `nohup ./script.sh &`  |
| `kill`       | Terminate processes               | `kill -9 1234`         |

**Signals Cheatsheet:**
- `SIGTERM (15)`: Graceful termination *(default)*  
- `SIGKILL (9)`: Force kill *(uncatchable)*  
- `SIGHUP (1)`: Reload configs  

**Detach Processes Like a Pro:**
```bash
screen -S mysession  # Start named session
./long_running_task
Ctrl+A → D           # Detach
screen -r mysession  # Reattach
```

---

### 2️⃣ **System Logs Deep Dive**  
#### Critical Log Files:
| Log Path                   | Purpose                 |
| -------------------------- | ----------------------- |
| `/var/log/syslog`          | General system events   |
| `/var/log/auth.log`        | Authentication attempts |
| `/var/log/kern.log`        | Kernel messages         |
| `/var/log/nginx/error.log` | Service-specific logs   |

**Journalctl (Systemd):**
```bash
journalctl -u sshd --since "1 hour ago"  # SSH logs
journalctl -p err -b  # Errors since last boot
journalctl -f        # Tail logs in real-time
```

**Log Filtering Tricks:**
```bash
grep "FAILED" /var/log/auth.log | awk '{print $11}' | sort | uniq -c
```

---

### 3️⃣ **Debugging Toolbelt**  
#### strace (System Calls):
```bash
strace -f -e trace=file ./program  # Trace file operations
strace -p 1234 -s 512             # Attach to running process
```
**Key Flags:**
- `-f`: Follow child processes  
- `-o`: Save to file  
- `-e trace=network`: Filter network calls  

#### ltrace (Library Calls):
```bash
ltrace -e malloc+free ./app  # Track memory allocations
```

#### gdb (Binary Debugging):
```bash
gdb -q ./target
(gdb) break main             # Set breakpoint
(gdb) run arg1 arg2          # Start program
(gdb) info registers         # Inspect CPU state
(gdb) backtrace              # Call stack trace
```

**GDB Cheatsheet:**
- `next` (n): Step over  
- `step` (s): Step into  
- `x/20x $rsp`: Examine stack memory  

---

### 4️⃣ **Advanced Process Inspection**  
#### /proc Filesystem:
```bash
cat /proc/1234/environ    # Process environment
ls -l /proc/1234/fd      # Open file descriptors
cat /proc/1234/cmdline   # Full command string
```

#### lsof (Open Files):
```bash
lsof -i :80              # Processes using port 80
lsof -u www-data         # Files opened by user
```

#### Network Debugging:
```bash
ss -tulnp                # Socket statistics
tcpdump -i eth0 'port 443' -w capture.pcap
```

---

### 5️⃣ **Real-World Debugging Flow**  
**Scenario:** Apache crashing intermittently  
1. **Logs First:**
   ```bash
   journalctl -u apache2 --no-pager -n 50
   ```
2. **Strace for System Calls:**
   ```bash
   strace -ff -o apache_trace /usr/sbin/apache2 -X
   ```
3. **Memory Analysis:**
   ```bash
   valgrind --leak-check=full ./apache_worker
   ```
4. **Binary Debugging:**
   ```bash
   gdb /usr/sbin/apache2 core.dump
   ```

---

### 6️⃣ **Performance Profiling**  
#### perf (CPU Analysis):
```bash
perf top -p 1234         # Real-time CPU usage
perf record -g ./program # Call graph capture
```

#### bpftrace (Kernel-Level):
```bash
bpftrace -e 'tracepoint:syscalls:sys_enter_* { @[probe] = count(); }'
```

---

### 7️⃣ **Security Considerations**  
**Dangerous Patterns to Audit:**
```bash
# World-writable SUID files
find / -perm -4007 -ls 2>/dev/null

# Suspicious process hiding
ps -ef | grep -v '\['
```

**Secure Logging:**
```bash
# Prevent log tampering
chattr +a /var/log/secure
```

---

### 8️⃣ **Exercises**  
1. **Strace Practice:**
   - Trace `ls -l` system calls:  
     ```bash
     strace -o trace.log ls -l
     ```
2. **GDB Challenge:**
   - Debug a segfaulting C program:  
     ```bash
     gdb ./crash_program
     (gdb) run
     (gdb) backtrace
     ```
3. **Log Detective:**
   - Find failed SSH attempts from `/var/log/auth.log`:  
     ```bash
     grep "Failed password" /var/log/auth.log | awk '{print $11}' | sort | uniq -c
     ```

---

### 9️⃣ **Pro Tips**  
- **Debugging Init Systems:**
  ```bash
  systemctl status --no-pager -l service
  ```
- **Persistent Logging:**
  ```bash
  sudo rsyslogd -N1  # Validate config
  ```
- **Container Debugging:**
  ```bash
  docker run --cap-add=SYS_PTRACE --security-opt seccomp=unconfined debian
  ```

---

### 🔖 Visual Cheatsheet  
```
# Process States
R: Running    S: Sleeping   D: Uninterruptible
Z: Zombie     T: Stopped

# Signal Quick Reference
1: HUP   2: INT   9: KILL   15: TERM
```

🚀 **Next-Level Debugging**:  
- *"Kernel Debugging with kgdb"*  
- *"eBPF for Advanced Tracing"*  