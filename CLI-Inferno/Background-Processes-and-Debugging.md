# 📝 Linuxda Fond Jarayonlari, Nosozliklarni Tuzatish va Jurnallar

---

## 1️⃣ **Jarayonlarni Boshqarish Asoslari**

### Asosiy Buyruqlar:
| Buyruq       | Tavsif                              | Misol                   |
| ------------ | ------------------------------------ | ------------------------ |
| `ps`         | Jarayonlar holatini ko‘rsatadi       | `ps aux \| grep nginx`  |
| `top`/`htop` | Interaktiv jarayonlar monitori       | `htop -u www-data`      |
| `jobs`       | Fond jarayonlar ro‘yxati             | `jobs -l`               |
| `bg`/`fg`    | Fonddan oldinga/oldingidan fondga    | `bg %1`                 |
| `nohup`      | Jarayonni uzilishga chidamli qiladi  | `nohup ./script.sh &`   |
| `kill`       | Jarayonni to‘xtatadi                 | `kill -9 1234`          |

### Signal Cheat Sheet:
- `SIGTERM (15)`: Oddiy to‘xtatish (default)
- `SIGKILL (9)`: Majburiy to‘xtatish (ushlab bo‘lmaydi)
- `SIGHUP (1)`: Konfiguratsiyani qayta yuklash

### Jarayonlarni Ajratish:
```bash
screen -S mysession
./long_running_task
Ctrl+A → D           # Ajratish
screen -r mysession  # Qayta ulanish
```

---

## 2️⃣ **Tizim Jurnallari (Loglar)**

### Muhim Log Fayllar:
| Log Yo‘li                   | Maqsad                        |
| --------------------------- | ----------------------------- |
| `/var/log/syslog`           | Umumiy tizim hodisalari       |
| `/var/log/auth.log`         | Autentifikatsiya urinishlari  |
| `/var/log/kern.log`         | Yadro (kernel) xabarlari      |
| `/var/log/nginx/error.log`  | Servisga oid xatoliklar       |

### `journalctl` bilan ishlash:
```bash
journalctl -u sshd --since "1 hour ago"
journalctl -p err -b
journalctl -f
```

### Loglarni Filtrlash:
```bash
grep "FAILED" /var/log/auth.log | awk '{print $11}' | sort | uniq -c
```

---

## 3️⃣ **Nosozliklarni Tuzatish Asboblari**

### `strace` (Tizim Chaqaruvlari):
```bash
strace -f -e trace=file ./program
strace -p 1234 -s 512
```

### Muhim Parametrlar:
- `-f`: Farzand jarayonlarini ham kuzatadi
- `-o`: Natijani faylga yozadi
- `-e trace=network`: Tarmoq chaqiruvlarini ko‘rsatadi

### `ltrace` (Kutubxona chaqiruvlari):
```bash
ltrace -e malloc+free ./app
```

### `gdb` (Ikkilik faylni nosozlikdan tozalash):
```bash
gdb -q ./target
(gdb) break main
(gdb) run arg1 arg2
(gdb) info registers
(gdb) backtrace
```

#### GDB Cheat Sheet:
- `next` (n): Keyingi qadam
- `step` (s): Ichkariga kirish
- `x/20x $rsp`: Stack xotirani tekshirish

---

## 4️⃣ **Jarayonlarni Tahlil Qilish**

### `/proc` katalogi:
```bash
cat /proc/1234/environ
ls -l /proc/1234/fd
cat /proc/1234/cmdline
```

### `lsof` (Ochiq fayllar):
```bash
lsof -i :80
lsof -u www-data
```

### Tarmoqni Tahlil Qilish:
```bash
ss -tulnp
tcpdump -i eth0 'port 443' -w capture.pcap
```

---

## 5️⃣ **Real Vaziyat: Apache Nosozligi**

### 1. Loglarni Ko‘rish:
```bash
journalctl -u apache2 --no-pager -n 50
```

### 2. `strace` bilan kuzatish:
```bash
strace -ff -o apache_trace /usr/sbin/apache2 -X
```

### 3. Xotira tahlili:
```bash
valgrind --leak-check=full ./apache_worker
```

### 4. `gdb` bilan tahlil:
```bash
gdb /usr/sbin/apache2 core.dump
```

---

## 6️⃣ **Ishlashni Profil qilish**

### `perf` bilan CPU tahlili:
```bash
perf top -p 1234
perf record -g ./program
```

### `bpftrace` bilan kernel kuzatuv:
```bash
bpftrace -e 'tracepoint:syscalls:sys_enter_* { @[probe] = count(); }'
```

---

## 7️⃣ **Xavfsizlik Masalalari**

### Xavfli Holatlarni Tekshirish:
```bash
find / -perm -4007 -ls 2>/dev/null
ps -ef | grep -v '\['
```

### Loglarni Himoyalash:
```bash
chattr +a /var/log/secure
```

---

## 8️⃣ **Amaliy Mashqlar**

### 1. `strace` Amaliyoti:
```bash
strace -o trace.log ls -l
```

### 2. `gdb` Mashqi:
```bash
gdb ./crash_program
(gdb) run
(gdb) backtrace
```

### 3. SSH Xatoliklarini Topish:
```bash
grep "Failed password" /var/log/auth.log | awk '{print $11}' | sort | uniq -c
```

---

## 9️⃣ **Mutaxassislar Uchun Maslahatlar**

### Init tizimlarni tahlil qilish:
```bash
systemctl status --no-pager -l service
```

### Doimiy loglashni yoqish:
```bash
sudo rsyslogd -N1
```

### Konteynerlarda nosozliklarni aniqlash:
```bash
docker run --cap-add=SYS_PTRACE --security-opt seccomp=unconfined debian
```

---

## 🔖 Vizual Cheat Sheet
```
# Jarayon Holatlari
R: Ishlayapti    S: Uyquda    D: Qaytmas (Uninterruptible)
Z: Zombie        T: To‘xtagan

# Signal Tezkor Ko‘rsatma
1: HUP   2: INT   9: KILL   15: TERM
```

🚀 **Keyingi Daraja:**
- "Kernel Debugging with kgdb"
- "eBPF bilan ilg‘or kuzatuv"

