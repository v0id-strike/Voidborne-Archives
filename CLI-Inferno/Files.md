### 1️⃣ **Asosiy navigatsiya buyruqlari**  
| Buyruq  | Tavsif                          | Misol                      |
| ------- | ------------------------------- | -------------------------- |
| `pwd`   | Joriy katalogni ko‘rsatadi      | `pwd` → `/home/user`       |
| `ls`    | Fayllarni ro‘yxatlaydi          | `ls -la` (yashirin fayllar) |
| `cd`    | Katalogni o‘zgartiradi          | `cd /var/log`              |
| `tree`  | Katalog tuzilmasini ko‘rsatadi  | `tree -L 2`                |

**Foydali maslahat:**  
```bash
cd -  # Oldingi katalogga qaytish
```

---

### 2️⃣ **Fayllar bilan ishlash**  
| Vazifa      | Buyruq     | Misol                          |
| ----------- | ---------- | ------------------------------ |
| Fayl yaratish | `touch`    | `touch notes.txt`              |
| Katalog yaratish | `mkdir -p` | `mkdir -p project/{src,docs}`  |
| Ko‘chirish / nomini o‘zgartirish | `mv`       | `mv old.txt new.txt`         |
| Nusxa olish | `cp -r`    | `cp -r dir1/ dir2/`            |
| O‘chirish   | `rm -rf`   | `rm -rf temp/`                 |

**Ogohlantirish:**  
❌ `rm -rf /` → **Havfli!** Har doim yo‘lni ikki marta tekshiring.

---

### 3️⃣ **Fayllarni qidirish**  
| Asbob     | Foydalanish holati    | Misol                             |
| --------- | --------------------- | --------------------------------- |
| `find`    | Murakkab qidiruvlar   | `find / -name "*.conf" -size +1M` |
| `locate`  | Tez nom bo‘yicha qidirish | `locate passwd`                   |
| `which`   | Ijro faylini topish   | `which python`                    |

**Muhim `find` parametrlar:**  
```bash
find /var/log -type f -mtime -7 -exec ls -lh {} \;
```
- `-type f`: Faqat fayllar  
- `-mtime -7`: So‘nggi 7 kunda o‘zgargan  
- `-exec`: Natijaga buyruqni qo‘llash  

---

### 4️⃣ **Fayl ichidagi matn va filtrlash**  
| Buyruq        | Funktsiya              | Misol                                |
| ------------- | ---------------------- | ------------------------------------- |
| `cat`         | Faylni ko‘rsatadi      | `cat /etc/passwd`                    |
| `grep`        | Matn izlash            | `grep "root" /etc/passwd`            |
| `head`/`tail` | Boshi yoki oxirini ko‘rish | `tail -n 20 log.txt`             |
| `awk`         | Ustunni ajratish       | `awk -F: '{print $1,$6}' /etc/passwd` |
| `sed`         | Matnni o‘zgartirish    | `sed 's/foo/bar/g' file.txt`         |

**Quvurlar kombinatsiyasi:**  
```bash
cat logs.txt | grep "ERROR" | awk '{print $2}' | sort | uniq -c
```

---

### 5️⃣ **Ruxsatlar bo‘yicha chuqur tushuncha**  
#### Ruxsat turlari:
| Belgisi | Fayl uchun       | Katalog uchun               |
| ------- | ---------------- | --------------------------- |
| `r`     | Mazmunni o‘qish  | Fayllar ro‘yxatini ko‘rish  |
| `w`     | O‘zgartirish     | Yaratish / o‘chirish        |
| `x`     | Ijro qilish      | Ichiga kirish               |

#### Sakkizlik yozuv:
| Raqam | Ruxsatlar                |
| ----- | ------------------------ |
| 7     | rwx (O‘qish+Yozish+Ijro) |
| 6     | rw- (O‘qish+Yozish)      |
| 5     | r-x (O‘qish+Ijro)        |

**Asosiy buyruqlar:**  
```bash
chmod 750 script.sh  # Egasi: rwx, Guruh: r-x, Boshqalar: --- 
chown user:group file
```

#### Maxsus ruxsatlar:
| Bit       | Ta’siri             | Misol                         |
| --------- | ------------------- | ----------------------------- |
| SUID (4)  | Egasi sifatida ishlaydi | `chmod 4755 /usr/bin/passwd` |
| SGID (2)  | Guruhni meros qiladi    | `chmod 2770 /shared`         |
| Sticky (1)| O‘chirishni cheklaydi   | `chmod 1777 /tmp`            |

---

### 6️⃣ **Yo‘naltirish va quvurlar**  
| Belgisi | Vazifasi           | Misol                        |
| ------- | ------------------ | ---------------------------- |
| `>`     | Faylni almashtirish | `ls > output.txt`            |
| `>>`    | Qo‘shib yozish      | `echo "new" >> log.txt`      |
| `2>`    | Xatoliklarni yozish | `cmd 2> errors.log`          |
| `|`     | Quvurlash           | `cat file | grep "text"`     |

**Kengaytirilgan yo‘naltirish:**  
```bash
command > >(tee stdout.log) 2> >(tee stderr.log >&2)
```

---

### 7️⃣ **Mashqlar**  
1. **Navigatsiya:**  
   - `/etc` ichidagi barcha `.conf` fayllarni hajm bo‘yicha saralang:  
     `ls -lS /etc/*.conf`  
   - `backups/{monthly,weekly}/2023` katalog tuzilmasini yarating  

2. **Ruxsatlar:**  
   - Barcha SUID fayllarni toping:  
     ```bash
     find / -perm -4000 2>/dev/null
     ```  
   - `/shared` katalogini quyidagicha sozlang:  
     - Guruh: `developers`  
     - Ruxsat: `rwxrwx---` (770)  

3. **Filtrlash:**  
   - `/etc/passwd` dan foydalanuvchi nomi va ularning shell'larini ajrating:  
     ```bash
     awk -F: '{print $1,$7}' /etc/passwd | column -t
     ```  

---

### 8️⃣ **Qo‘shimcha maslahatlar**  
- **Xavfsiz fayl ko‘chirish:** Katta fayllar uchun `rsync -avz` dan foydalaning  
- **Ruxsat kalkulyatori:**  
  ```bash
  stat -c "%a %n" *  # Barcha fayllar uchun sakkizlik ruxsatlar
  ```  
- **Tez arxivlash:**  
  ```bash
  tar -czvf backup.tar.gz /path/to/files
  ```  

---

### 9️⃣ **Vizual ko‘makchi**  
```
# Ruxsatlar tafsiloti
-rwxr-xr--  1 user group  size date filename
│└─┬─┘└─┬─┘
│ │  │   └── Boshqalar: r--
│ │  └────── Guruh: r-x
│ └───────── Egasi: rwx
└─────────── Fayl turi (-,d,l)
```
