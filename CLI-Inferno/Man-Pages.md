## **1️⃣ Manual Sahifalari (`man`)**
Linux'ning o‘z ichiga olingan hujjat tizimi `man` buyrug‘i orqali ochiladi.

### **Asosiy Xususiyatlari**
- **Tuzilgan bo‘limlar** (1-9): turli buyruq turlari uchun
- **Tez ko‘rsatma**: buyruqlar, konfiguratsiya fayllari, tizim chaqiriqlari
- **Offline mavjudligi**: barcha Linux tizimlarida mavjud

### **Foydalanish**
```bash
man [bo‘lim] buyruq
```

### **Misollar**
```bash
man ls           # Oddiy buyruq hujjati
man 5 passwd     # /etc/passwd fayl formati hujjati
man 3 printf     # C kutubxonasi funksiyasi hujjati
```

### **`man` sahifalarida harakat**
| Tugma      | Harakat                |
| ---------- | ---------------------- |
| `Space`    | Keyingi sahifaga o‘tish|
| `Enter`    | Keyingi qator          |
| `/pattern` | Oldinga qidirish       |
| `?pattern` | Orqaga qidirish        |
| `n`        | Keyingi moslik         |
| `q`        | Chiqish                |

### **Tegishli `man` sahifalarini topish**
```bash
man -k "network"          # Barcha `man` sahifalarida izlash
man -f passwd             # 'passwd' uchun barcha bo‘limlarni ko‘rsatish
whatis ls                 # Buyruq haqida qisqacha ma'lumot
```

---

## **2️⃣ Info Sahifalari (`info`)**
Ko‘proq tafsilotga ega hujjat tizimi, ko‘pincha gipermurojaat bilan birga keladi.

### **Asosiy Xususiyatlari**
- **Ierarxik hujjatlar**: tugunlar bilan tuzilgan
- **`man` sahifalaridan batafsilroq**: ayniqsa murakkab vositalar uchun
- **Gipermurojaat bilan navigatsiya**: bog‘langan mavzular orasida harakat

### **Foydalanish**
```bash
info buyruq
```

### **`info`da harakat**
| Tugma   | Harakat                  |
| ------- | ------------------------ |
| `n`     | Keyingi tugun            |
| `p`     | Oldingi tugun            |
| `u`     | Bir darajaga yuqoriga   |
| `Enter` | Havolaga kirish          |
| `Tab`   | Keyingi havolaga sakrash |
| `q`     | Chiqish                  |

### **Misollar**
```bash
info coreutils            # GNU core utilities hujjatlari
info emacs                # Emacs haqida batafsil qo‘llanma
info bash                 # Bash to‘liq hujjati
```

---

## **3️⃣ Onlayn Hujjatlar**
### **Tizim Hujjatlari**
```bash
/usr/share/doc/           # Paket hujjatlari joylashgan joy
less /usr/share/doc/package/README
```

### **Buyruq yordam parametrlari**
```bash
command --help            # Tez ko‘rsatma (GNU uslubi)
command -h                # Tez ko‘rsatma (BSD uslubi)
```

### **Paket hujjatlari**
```bash
dpkg -L package | grep doc  # Debian paketlari uchun hujjatlarni topish
rpm -qd package             # RPM paketlarining hujjatlarini ko‘rsatish
```

---

## **4️⃣ Taqqoslash: `man` va `info`**

| Xususiyat      | `man` Sahifalar | `info` Sahifalar      |
| -------------- | --------------- | ---------------------- |
| Tafsilot darajasi | Qisqacha     | Batafsil               |
| Harakat          | Linear        | Gipermurojaatli        |
| Mavjudlik        | Har doim      | Asosan GNU vositalari  |
| O‘rganish darajasi| Osonroq      | Murakkabroq            |
| Misollar         | Kam           | Ko‘p                   |

---

## **5️⃣ Hujjatlar bilan ishlash bo‘yicha maslahatlar**
1. **Tez ko‘rish uchun `--help`** dan boshlang
2. **Buyruqlar sintaksisi uchun `man`** dan foydalaning
3. **GNU vositalari uchun `info`** orqali chuqurroq o‘rganing
4. **`/usr/share/doc`** ichidan paketga xos hujjatlarni tekshiring
5. **Internetda qo‘llanmalar va misollarni izlang**

---

## **6️⃣ Hujjatlarni topish**
### **O‘rnatilgan buyruqlar uchun**
```bash
type command              # Buyruq qayerdan ishga tushadi
command --version         # Versiyasini ko‘rish
```

### **Tizim komponentlari uchun**
```bash
man hier                  # Fayl tizimi tuzilmasi haqida
man 7 glob                # Fayl nomi mosligi bo‘yicha
man 7 signal              # Linux signallari haqida
```

---

## **7️⃣ Kengaytirilgan maslahatlar**
- **Barcha man sahifalarida izlash**: `man -K "kalit so‘z"`
- **Man sahifasini PDF qilib chiqarish**: `man -t bash | ps2pdf - bash.pdf`
- **Siqilgan hujjatlarni ko‘rish**: `zless /usr/share/doc/package/README.gz`
- **O‘zingizning `man` sahifalaringizni yaratish**: `~/man/man1/` ichiga saqlang

---

## **8️⃣ Tavsiya etilgan Onlayn Manbalar**
1. **Linux man sahifalari**: [man7.org](https://man7.org/linux/man-pages/)
2. **GNU hujjatlari**: [www.gnu.org/manual](https://www.gnu.org/manual/)
3. **TLDR sahifalari**: [tldr.sh](https://tldr.sh/) (Soddalashtirilgan man sahifalari)
4. **Arch Linux Wiki**: [wiki.archlinux.org](https://wiki.archlinux.org/)
5. **Stack Overflow**: [stackoverflow.com](https://stackoverflow.com/)

🧠 **Eslab qoling:** Hujjatni tez va samarali topa olish hamda tushunish — har qanday Linux foydalanuvchisi yoki administratorining eng muhim ko‘nikmalaridan biridir!

