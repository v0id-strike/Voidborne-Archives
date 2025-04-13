
## 3️⃣ Sintaksisni tushuntirish

✅ `#!/bin/bash` → Shebang bu skriptni bajaradigan interpretatorni ko‘rsatadi.  
✅ `o'zgaruvchi="qiymat"` → O'zgaruvchilar ma'lumot saqlaydi (= atrofida bo'shliq bo'lmasligi kerak).  
✅ `if [ shart ]; then` → Shartli operatorlar test uchun kvadrat qavs ishlatadi.  
✅ `for item in list; do` → Takrorlash operatori ro‘yxat/array ustida aylanishni bajaradi.  
✅ `read -p "So‘rov: " var` → Foydalanuvchi kiritgan qiymat `var`ga yoziladi.  

## 4️⃣ Nima uchun / Qachon ishlatiladi

| Vaziyat                          | Bash | Python/C |
|----------------------------------|------|----------|
| Tezkor tizim avtomatlashtirish   | ✅   | ❌       |
| Buyruq natijasini tahlil qilish  | ✅   | ⚠️       |
| Murakkab ma'lumot tuzilmalari    | ❌   | ✅       |

**Eng yaxshi holatlar uchun:**  
- Unix buyruqlarini birlashtirish (grep, awk, whois)  
- Penetratsion testlar uchun tezkor prototiplash (masalan, hostni aniqlash)

## 5️⃣ Misollar

**Misol 1: Oddiy skript**  
```bash
#!/bin/bash  
echo "Salom, $USER!"  
```

**Misol 2: IP-finder.sh**  
```bash
#!/bin/bash  AIga ulangan tg-bot yarating (mening ko'rsatmalarim)
Siz TG botini yaratishingiz va unga chatZhPT yoki Claude Sonnet (men sizga API beraman) ulanishingiz kerak.
Bizga allaqachon shunga o'xshash ishni qilgan mutaxassis kerak (chunki bu juda oddiy, hatto Klod Sonnetning o'zi ham kodni yozadi va nima qilish kerakligini bosqichma-bosqich tushuntiradi ... lekin biz odam buni tushunishini va buni birinchi marta qilmasligini istaymiz).
domain=$1  
ip=$(host $domain | grep "has address" | cut -d" " -f4)  
echo "Topilgan IP: $ip"  
```

## 6️⃣ Kengaytirilgan ishlatish / Foydali usullar

**Pattern Matching:**  
```bash
case $opt in  
    [Yy]*) echo "Ha" ;;  
    [Nn]*) echo "Yo‘q" ;;  
esac  
```

**Buyruq natijasini olish:**  
```bash
cidr=$(whois $ip | grep "CIDR")  
```

## 7️⃣ Maslahatlar va xatoliklar

❌ Bo‘shliq bilan o‘zgaruvchi: `var = "qiymat"` (noto‘g‘ri) vs `var="qiymat"` (to‘g‘ri)  
✅ Debug uchun: `set -x` ishlating  
❌ `case` blokida `;;` ni unutish sintaksis xatolarga olib keladi  

## 8️⃣ Xulosa

Bash skriptlar tizim ishlarini avtomatlashtirish uchun ideal, ayniqsa xavfsizlik sohasida (host topish, loglarni tahlil qilish). U soddalikni kuchli buyruq satri bilan birlashtiradi.

## 🔖 Bonus

- Portativlik uchun `#!/usr/bin/env bash` ishlating  
- Rangli chiqish:  
```bash
echo -e "\e[31mXatolik\e[0m"  # Qizil matn
```

---AIga ulangan tg-bot yarating (mening ko'rsatmalarim)
Siz TG botini yaratishingiz va unga chatZhPT yoki Claude Sonnet (men sizga API beraman) ulanishingiz kerak.
Bizga allaqachon shunga o'xshash ishni qilgan mutaxassis kerak (chunki bu juda oddiy, hatto Klod Sonnetning o'zi ham kodni yozadi va nima qilish kerakligini bosqichma-bosqich tushuntiradi ... lekin biz odam buni tushunishini va buni birinchi marta qilmasligini istaymiz).

# 📌 2-bosqich: Shartli bajarish

## 1️⃣ Kirish / Ta’rif

Shartli bajarish skriptga holatlarga qarab turli yo‘nalishda ishlash imkonini beradi. Agar bu bo‘lmasa, kod faqat ketma-ket bajariladi. Asosiy tuzilmalar:  
- `if-then-fi` → Asosiy shart tekshiruvi  
- `elif` → Qo‘shimcha shartlar  
- `else` → Hech biri to‘g‘ri bo‘lmasa bajariladi  

## 2️⃣ Sintaksis

**Asosiy tuzilma:**  
```bash
if [ shart ]; then  AIga ulangan tg-bot yarating (mening ko'rsatmalarim)
Siz TG botini yaratishingiz va unga chatZhPT yoki Claude Sonnet (men sizga API beraman) ulanishingiz kerak.
Bizga allaqachon shunga o'xshash ishni qilgan mutaxassis kerak (chunki bu juda oddiy, hatto Klod Sonnetning o'zi ham kodni yozadi va nima qilish kerakligini bosqichma-bosqich tushuntiradi ... lekin biz odam buni tushunishini va buni birinchi marta qilmasligini istaymiz).
    # Agar rost bo‘lsa  
elif [ shart ]; then  
    # Agar elif rost bo‘lsa  
else  
    # Hech biri rost bo‘lmasa  
fi  
```

**Misol: Argumentni tekshirish**  
```bash
if [ $# -eq 0 ]; then  
    echo "Xatolik: Argumentlar kiritilmagan."  
    exit 1  
fi  
```

## 3️⃣ Sintaksis tushuntirish

✅ `if [ shart ]` → Shartli blokni boshlaydi. [ va ] atrofida bo‘shliq bo‘lishi shart.  
✅ `-eq`, `-lt`, `-gt` → Taqqoslash operatorlari (=, <, >)  
✅ `$#` → Foydalanuvchi kiritgan argumentlar soni  
✅ `exit 1` → Xatolik kodi bilan chiqish  

## 4️⃣ Nima uchun / Qachon ishlatiladi

| Vaziyat                     | Ishlatish            |
|-----------------------------|-----------------------|
| Foydalanuvchi kiritishini tekshirish | `if [ $# -eq 0 ]`     |
| Turli holatlarni boshqarish         | `if-elif-else` zanjiri |
| Xatolikni boshqarish                | `exit` bilan chiqish   |

**Asosiy foydasi:** noto‘g‘ri kiritishlar tufayli skript buzilmasligini ta’minlaydi.

## 5️⃣ Misollar

**Misol 1: Sonni solishtirish**  
```bash
value=$1  
if [ $value -gt 10 ]; then  
    echo "Qiymat > 10"  
elif [ $value -lt 10 ]; then  
    echo "Qiymat < 10"  
else  
    echo "Qiymat = 10"  
fi  
```

**Misol 2: Fayl borligini tekshirish**  
```bash
if [ -f "file.txt" ]; then  
    echo "Fayl mavjud."  
else  
    echo "Fayl topilmadi."  
fi  
```

## 6️⃣ Kengaytirilgan ishlatish / Foydali usullar

**Shartlarni birlashtirish:**  
```bash
if [ $yosh -gt 18 ] && [ "$mamlakat" = "US" ]; then  
    echo "Mos keladi."  
fi  
```

**Regex bilan tekshirish:**  
```bash
if [[ "$kiritma" =~ ^[A-Za-z]+$ ]]; then  
    echo "Faqat harflardan iborat."  
fi  
```

## 7️⃣ Maslahatlar va xatoliklar

❌ Bo‘shliqsiz yozish: `if[$#-eq0]` → Xatolik  
✅ O‘zgaruvchilarni qo‘shtirnoqda yozing: `if [ "$var" = "qiymat" ]` → So‘z ajralishining oldini oladi  
❌ Sonlar uchun `=` ishlatmang: `-eq` ishlating  

## 8️⃣ Xulosa

Shartli operatorlar (if-elif-else) skriptlarni dinamik va foydalanuvchi kiritishiga mos qiladi. Har doim chekka holatlarni test qiling!

## 🔖 Bonus

- Kengaytirilgan imkoniyatlar uchun `[[]]` ishlating (`[]` o‘rniga)  
- Rangli xatoliklar:  
```bash
echo -e "\e[31mXatolik: Argumentlar yo‘q.\e[0m"
```
