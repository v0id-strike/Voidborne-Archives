# 3-bosqich: O'zgaruvchilar, Argumentlar va Massivlar

## 1️⃣ Kirish / Ta’rif
Bash foydalanuvchi tomonidan kiritilgan buyruq argumentlarini avtomatik ravishda $0–$9, $#, $@ kabi maxsus o‘zgaruvchilar orqali boshqaradi. O‘zgaruvchilar odatda matnli qiymatlarni saqlaydi. Massivlar esa bir nechta qiymatlarni saqlashga imkon beradi. Ushbu imkoniyatlar skriptlarni foydalanuvchi kirituvi asosida moslashuvchan qiladi.

## 2️⃣ Sintaksis Blok

### Buyruq satri argumentlari:
```
$0          # Skript nomi
$1-$9       # 1-dan 9-gacha argumentlar
${10}       # 10 va undan yuqori argumentlar uchun {} kerak
```

### O‘zgaruvchi tayinlash:
```
var="qiymat"   # To‘g‘ri (bo‘sh joysiz)
var = "qiymat" # Noto‘g‘ri (xato beradi)
```

### Massiv e’lon qilish:
```
arr=("val1" "val2" "val3")  # Indeks 0 dan boshlanadi
echo ${arr[1]}              # Ikkinchi elementni chiqarish
```

## 3️⃣ Sintaksis tushuntirishi

✅ `$0` → Har doim skript nomini o‘z ichiga oladi.  
✅ `$1`, `$2`... → Pozitsion argumentlar ($9 gacha). 10-dan keyin `${10}` shaklida yoziladi.  
✅ `var="qiymat"` → Tayinlashda `=` atrofida bo‘sh joy bo‘lmasligi kerak.  
✅ `arr=(...)` → Massivlar `()` orqali e’lon qilinadi, va qiymatlar bo‘shliq bo‘lsa `"..."` bilan olinadi.

## 4️⃣ Qachon va nima uchun foydalaniladi

| VAZIYAT                | FOYDALANILADIGAN ELEMENT        |
|------------------------|----------------------------------|
| Foydalanuvchi kirituvi | `$1`, `$2`, `$@`                |
| Bir nechta qiymat      | Massivlar `arr=(...)`           |
| Kirituvni tekshirish   | `$#` (argumentlar soni)         |
| Skriptni tahlil qilish | `$?` (chiqish holati kodi)      |

**Asosiy foyda**: Skriptni foydalanuvchi kirituvi asosida moslashuvchan ishlashini ta’minlaydi.

## 5️⃣ Misollar

### Misol 1: Oddiy argument ishlatish
```bash
#!/bin/bash
echo "Skript: $0"
echo "Birinchi argument: $1"
echo "Barcha argumentlar: $@"
```

### Misol 2: Massivdan foydalanish
```bash
domains=("www.example.com" "ftp.example.com")
echo "Birinchi domain: ${domains[0]}"
echo "Barcha domainlar: ${domains[@]}"
```

## 6️⃣ Kengaytirilgan foydalanish / Fokuslar

### Argumentlarni siljitish:
```bash
shift   # $1 o‘chiriladi, qolganlari chapga siljiydi ($2 → $1)
```

### Standart qiymatlar:
```bash
name=${1:-"Mehmon"}  # Agar $1 bo‘sh bo‘lsa, "Mehmon" olinadi
```

### Assotsiativ massivlar (Bash 4+):
```bash
declare -A colors=(["qizil"]="#FF0000" ["yashil"]="#00FF00")
echo ${colors["qizil"]}
```

## 7️⃣ Maslahatlar va keng tarqalgan xatolar

❌ E’lon qilinmagan o‘zgaruvchilar: `rm $file` xato beradi, agar `$file`da bo‘shliq bo‘lsa. **To‘g‘ri**: `rm "$file"`  
✅ Argumentlar sonini tekshirish:
```bash
if [ $# -lt 2 ]; then echo "2 ta argument kerak"; exit 1; fi
```  
❌ Qavslar yo‘q: `$10` → `$1` + `0` sifatida talqin qilinadi. **To‘g‘ri**: `${10}`

## 8️⃣ Xulosa

Bash'dagi maxsus o‘zgaruvchilar (`$0–$9`, `$#`, `$@`) va massivlar foydalanuvchi kirituvi bilan ishlashda juda foydali. O‘zgaruvchilar odatda matn shaklida bo‘ladi. Massivlar esa bir nechta qiymatni saqlashni osonlashtiradi. Har doim kirituvni tekshiring!

## 🔖 Bonus

### Barcha argumentlarni ro‘yxatlash:
```bash
for arg in "$@"; do echo "$arg"; done
```

### Massivni kesib olish (slice):
```bash
echo ${arr[@]:1:3}  # 1 dan 3 gacha bo‘lgan elementlar
```