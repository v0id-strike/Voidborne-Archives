
# 🧠 4-bosqich: Taqqoslash operatorlari (Comparison Operators)

## 1️⃣ Kirish / Ta’rif
Bash skriptlarda taqqoslash operatorlari shartlarni baholash orqali qarorlar qabul qilish imkonini beradi. Ular quyidagi toifalarga bo‘linadi:

- **Satr operatorlari** (matn solishtirish)
- **Butun son operatorlari** (raqam solishtirish)
- **Fayl operatorlari** (fayl tizimini tekshirish)
- **Mantiqiy operatorlar** (shartlarni birlashtirish)

---

## 2️⃣ Sintaksis blok

**Satr solishtirish:**
```bash
[ "$var" == "value" ]     # Tenglik
[[ "$var" > "A" ]]         # ASCII bo‘yicha solishtirish (faqat [[ ]] bilan)
```

**Butun son solishtirish:**
```bash
[ $num -lt 10 ]           # 10 dan kichik
```

**Fayl tekshiruvi:**
```bash
[ -f "file.txt" ]         # Oddiy fayl mavjudmi
```

**Mantiqiy operatorlar:**
```bash
[ "$var" ] && [ -f "$var" ]              # AND
[[ -z "$var" || ! -d "$dir" ]]           # OR/NOT
```

---

## 3️⃣ Sintaksis izohi

✅ **Qo‘shtirnoq muhim**: `"$var"` bo‘sh yoki ichida bo‘shliq bo‘lsa, xatolarning oldi olinadi.  
✅ **[[ ]]** – kengaytirilgan ifodalar va &&/|| qo‘llab-quvvatlaydi.  
✅ **Fayl operatorlari**: `-e`, `-f`, `-d` – mavjudlik va turini tekshiradi.

---

## 4️⃣ Qachon va nima uchun ishlatiladi

| VAZIYAT                  | Operator turi       | Misol                        |
|-------------------------|---------------------|------------------------------|
| Foydalanuvchini tekshirish | Satr (==, !=)      | `[ "$1" == "admin" ]`        |
| Raqam oraliqlarini tekshirish | Integer (-lt, -gt) | `[ $age -ge 18 ]`            |
| Fayl ruxsatlarini tekshirish | Fayl (-r, -w)       | `[ -w "/etc/passwd" ]`       |
| Murakkab shartlar         | Mantiqiy (&&/||)     | `[ -f "$file" ] && [ -s "$file" ]` |

---

## 5️⃣ Misollar

**Misol 1: Satr solishtirish**
```bash
if [ "$USER" != "root" ]; then
    echo "Xato: root sifatida ishga tushiring!"
    exit 1
fi
```

**Misol 2: Fayl mavjudligini tekshirish**
```bash
if [[ -f "$logfile" && -s "$logfile" ]]; then
    echo "Log fayli mavjud va bo‘sh emas."
fi
```

**Misol 3: Raqam oraliqlari**
```bash
if [ $count -gt 0 ] && [ $count -le 100 ]; then
    echo "Yaroqli son (1-100)."
fi
```

---

## 6️⃣ Ilg‘or qo‘llanma / Fintlar

**Shablonlarga moslik:**
```bash
if [[ "$file" == *.txt ]]; then
    echo "Matnli fayl topildi."
fi
```

**Birgalikda tekshirish:**
```bash
[ -d "$dir" ] || mkdir -p "$dir"  # Agar yo‘q bo‘lsa, katalog yaratiladi
```

---

## 7️⃣ Foydali maslahatlar va xatoliklar

❌ **Qo‘shilmagan qo‘shtirnoqlar**: `[ $var == "value" ]` – `$var` bo‘sh bo‘lsa, xatolik.  
✅ **[[ ]] ishlatish** – xavfsizroq va regexni qo‘llab-quvvatlaydi.  
❌ **Operatorlarni aralashtirmang**: raqamlar uchun `-eq`, satrlar uchun `==`.

---

## 8️⃣ Xulosa

Taqqoslash operatorlari quyidagi uchun muhim:

- Kiritilgan ma’lumotni tekshirish (satr/raqam)
- Fayllarni va ruxsatlarni aniqlash
- Murakkab mantiqiy qarorlar yaratish

Har doim o‘zgaruvchilarni qo‘shtirnoqqa oling va `[[ ]]` ustunligini biling!

---

## 🔖 Bonus

**Regex bilan solishtirish:**
```bash
if [[ "$email" =~ ^[A-Za-z0-9._%+-]+@[A-Za-z0-9.-]+\.[A-Za-z]{2,}$ ]]; then
    echo "Yaroqli email."
fi
```

**Chiqish kodini tekshirish:**
```bash
if grep -q "error" logfile; then
    echo "Xatoliklar topildi!"
fi
```
