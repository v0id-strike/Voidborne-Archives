# 1-bosqich: Bash skriptlariga kirish

## 1️⃣ Kirish / Ta’rif
**Bash** — bu Unix shell va buyruq tili bo‘lib, avtomatlashtirish, tizim boshqaruvi hamda penetratsion testlarda keng qo‘llaniladi. Kompilyatsiya talab qilmaydi, shuning uchun tez va moslashuvchan ishlaydi. Asosiy xususiyatlari:

- Kompilyatsiya talab qilinmaydi  
- Tizim buyruqlari bilan bevosita integratsiya  
- Xavfsizlikdagi vazifalar (privilege escalation, ma’lumotlarni filtrlash) uchun muhim

---

## 2️⃣ Sintaksis blok

**Asosiy skript tuzilmasi:**

```bash
#!/bin/bash  
# Izohlar '#' bilan boshlanadi  

# O'zgaruvchilar  
o'zgaruvchi="qiymat"  

# Funksiyalar  
funksiya_nomi() {  
    buyruqlar  
}  

# Shartli bajarish  
if [ shart ]; then  
    buyruqlar  
fi  

# Sikllar  
for element in ro'yxat; do  
    buyruqlar  
done  

# Foydalanuvchi kirituvi  
read -p "So'rov: " o'zgaruvchi  


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
# 5-bosqich: Aritmetik operatorlar

Bash tilida butun sonlar ustida matematik amallarni bajarish va o‘zgaruvchilar qiymatini o‘zgartirish uchun 7 ta arifmetik operator mavjud.

Operator | Tavsif
---------|--------
+        | Qo‘shish
-        | Ayirish
*        | Ko‘paytirish
/        | Bo‘lish
%        | Qoldiqni olish (Modulus)
variable++ | 1 ga oshirish
variable-- | 1 ga kamaytirish

Arifmetik hisob-kitoblar uchun `$(())` sintaksisidan foydalaniladi.

Misol:

```bash
#!/bin/bash

oshirish=1
kamaytirish=1

echo "Qo‘shish: 10 + 10 = $((10 + 10))"
echo "Ayirish: 10 - 10 = $((10 - 10))"
echo "Ko‘paytirish: 10 * 10 = $((10 * 10))"
echo "Bo‘lish: 10 / 10 = $((10 / 10))"
echo "Modulus: 10 % 4 = $((10 % 4))"

((oshirish++))
echo "O'zgaruvchini oshirish: $oshirish"

((kamaytirish--))
echo "O'zgaruvchini kamaytirish: $kamaytirish"
```

Natija:

```bash
Qo‘shish: 10 + 10 = 20
Ayirish: 10 - 10 = 0
Ko‘paytirish: 10 * 10 = 100
Bo‘lish: 10 / 10 = 1
Modulus: 10 % 4 = 2
O'zgaruvchini oshirish: 2
O'zgaruvchini kamaytirish: 0
```
Misol:

```bash
#!/bin/bash

htb="HackTheBox"

echo "Matn uzunligi: ${#htb}"
```
Natija:
```
10
```
Misol:
```
echo -e "\nHost(lar)ga ping yuborilmoqda:"
for host in $cidr_ips; do
    stat=1
    while [ $stat -eq 1 ]; do
        ping -c 2 $host > /dev/null 2>&1
        if [ $? -eq 0 ]; then
            echo "$host faol."
            ((stat--))
            ((hosts_up++))
            ((hosts_total++))
        else
            echo "$host faol emas."
            ((stat--))
            ((hosts_total++))
        fi
    done
done
```
Izohlar:

- ((stat--)) — sikl oxir-oqibat tugashi uchun ishlatiladi

- ((hosts_up++)) — faol hostlar sonini oshiradi

- ((hosts_total++)) — umumiy tekshirilgan hostlar hisobini yuritadi

# 6-bosqich: Aritmetik operatorlar

## 1️⃣ Kirish / Ta’rif

Bash tilida butun sonlar asosida arifmetik amallarni bajarish uchun `$(( ))` va `(( ))` sintaksislari mavjud. Asosiy imkoniyatlar:

- Oddiy hisob-kitoblar: `+`, `-`, `*`, `/`, `%`
- Avtomatik inkrement/dekrement: `++`, `--`
- Satr uzunligini tekshirish: `${#o'zgaruvchi}`
- Sikllarni boshqarish va tarmoq operatsiyalari (masalan, hostlarni skanerlash) uchun juda muhim

---

## 2️⃣ Sintaksis Bloki

**Oddiy hisoblash:**

```bash
echo "$((5 + 3))"     # → 8
echo "$((5 / 2))"     # → 2 (butun sonli bo‘lish)
```
Ayirish/Qo'shish
```
((counter++))         # Post-inkrement — avvalgi qiymatdan foydalanadi, keyin 1 ga oshiradi
((--total))           # Pre-dekrement — avval 1 ga kamaytiradi, keyin qiymatdan foydalanadi
```
Satr uzunligi:
```
str="Hello"
echo "${#str}"        # → 5
```
### 3️⃣ **Sintaksisni tushuntirish**
- ✅ ` $(( )) ` → Natijani hisoblab chiqaradi (echo, o‘zgaruvchiga tayinlashda ishlatiladi).
- ✅ ` (( )) ` → Hisoblaydi, lekin natijani chiqarib bermaydi (sikl yoki shartlarda foydali).
- ✅ ` ${#var} ` → Satr uzunligini (bo‘sh joylar bilan) qaytaradi.
- ❌ **Floating-point (kasr sonlar)** yo‘q: buning uchun ` bc ` yoki ` awk ` dan foydalaniladi.

### 4️⃣ **Qachon va nima uchun ishlatiladi**
```
#!/bin/bash
read -p "Ikkita son kiriting: " a b
echo "Yig‘indi: $((a + b))"
echo "Ko‘paytma: $((a * b))"
```

### 5️⃣ **Misollar**
#### 1-misol: Oddiy kalkulyator
```
#!/bin/bash
read -p "Ikkita son kiriting: " a b
echo "Yig‘indi: $((a + b))"
echo "Ko‘paytma: $((a * b))"
```
#### 2-misol: Parol kuchini tekshirish
```
password="P@ssw0rd"
if [ ${#password} -lt 8 ]; then
    echo "Kuchsiz: Parol juda qisqa!"
fi
```
#### 3-misol: CIDR host skanerlovchi (parcha)
```
for ip in $cidr_ips; do
    ping -c 1 $ip >/dev/null && ((alive++))
    ((total++))
done
echo "$alive/$total hostlar javob berdi."
```
### 6️⃣ **Kengaytirilgan foydalanish / Fintlar**
- **Bit bo‘yicha operatsiyalar**:
```
echo "$((5 & 3))"   # AND → 1
echo "$((16#FF))"   # O‘n oltilikdan o‘nlikka → 255
```
- **Kasr sonlar bilan ishlash**:
```
echo "scale=2; 10/3" | bc  # → 3.33
```
- **Tasodifiy sonlar**:
```
echo $((RANDOM % 100))  # 0 dan 99 gacha
```
### 7️⃣ **Maslahatlar va keng tarqalgan xatoliklar**
- ❌ **O‘rnatishda bo‘sh joy**: ` sum = $((a+b)) ` xato ` sum=$((a+b)) `   to‘g‘ri
- ✅ **Xatolik yuz bersa, chiqish**:
```
((count > 0)) || exit 1 # Agar count ≤ 0 bo‘lsa, chiqadi
```
❌ **Satrlarni ` [ ] ` ichida qo‘shtirnaksiz ishlatish**: ` [[ "${var}" == value ]] ` xavfsizroq

### 8️⃣ **Xulosa**
> Bash arifmetikasining imkoniyatlari:

> - **Sikllarni samarali boshqarish** (hisoblagichlar, chiqish shartlari)

> - **Tarmoq operatsiyalari** (hostlarni skanerlash, IP hisoblash)

> - **Kiritilgan qiymatlarni tekshirish** (uzunlik, son oraliqlari)

> Bularni sikllar va shartlar bilan birlashtirib, kuchli avtomatlashtirishlarni yaratish mumkin!

---

### 🔖 Bonus: Pro maslahatlar
**Ternary (uchlik) operatsiya**:
```
(( result = condition ? 1 : 0 ))  Agar shart to‘g‘ri bo‘lsa, result o‘zgaruvchiga 1 qiymati beriladi, aks holda 0
```
**Terminalda tez hisoblash**:
```
echo $(( (10 + 5) * 2 ))  # → 30
```
## **📌 7-foyda: Kirish va Chiqish Nazorati
### 1️⃣ **Kirish / Ta'rif**
> Bash quyidagi kuchli vositalarni taqdim etadi:

> - **Skriptni boshqarish** uchun interaktiv kirish (` read `)

> - **Chiqish nazorati** (`>`, `>>`, `2>`) va `tee` orqali

> - **Holat bayonotlari** (`case`) yordamida oqimni boshqarish

Foydalanuvchiga qulay skriptlar yaratish va natijalarni qayd etish uchun zarur.

### 2️⃣ **Sintaksis bloklari**
#### Foydalanuvchi kirishi:
```
read -p "So'rov: " variable  # $variable o'zgaruvchisiga foydalanuvchi kiritgan ma'lumotni saqlaydi
```
#### Chiqishni yo‘naltirish:
```
command > file.txt      # Faylni o‘zgartirish
command >> file.txt     # Faylga qo‘shish
command 2> errors.log   # Xatoliklarni yo‘naltirish
command &> output.log   # Barcha chiqishlarni yo‘naltirish
```
#### Tee yordamida ikki yo‘nalishli chiqish:
```
command | tee file.txt      # Chiqishni ko‘rsatish va faylga yozish
command | tee -a file.txt   # Chiqishni ko‘rsatish va faylga qo‘shish
```
#### Case bayonoti:
```
case $var in
    "1") command1 ;;
    "2") command2 ;;
    *) default_command ;;
esac
```
### 3️⃣ **Sintaksis izohlarini tushuntirish**
- ✅ ` read -p ` → Foydalanuvchidan so‘rov olish va kiritilgan ma'lumotni saqlash (masalan, menyu tanlovlari).
- ✅ `tee` → Chiqishni terminalga va faylga bir vaqtning o‘zida chiqaradi (-a opsiyasi faylga qo‘shish qiladi).
- ✅ `case` → Ko‘p shartlar uchun joylashgan if bayonotlaridan yaxshiroq variant.
- ❌ `read` **komandasidagi qo'shtirnoqsiz o'zgaruvchilar**: So'zlarni ajratish muammolariga olib kelishi mumkin.
### 4️⃣ **Nega / Qachon ishlatish kerak**

|        Vaziyat                 |     Vosita         |      Misol                           |                 |
| ------------------------------ | ------------------ | ------------------------------------ | --------------- |
| Interaktiv menyular            | `read` + `case`    | CIDR.sh opsiyalari                   |                 |
| Komanda chiqishini qayd qilish | `tee`              | `whois $ip                           | tee -a log.txt` |
| Xatoliklarni boshqarish        | `2>`               | `cmd 2> errors.log`                  |                 |
| Jarayonning ko‘rinishi         | `tee` yoki `-a`    | Real vaqtda skanerlash yangiliklari  |                 |

### 5️⃣ **Misollar**
#### Misol 1: Interaktiv menyu
```
read -p "Tanlang (1-Skanerlash, 2-Ping): " opt
case $opt in
    1) nmap -sV $target ;;
    2) ping -c 4 $target ;;
    *) echo "Noto‘g‘ri tanlov" ;;
esac
```
#### Misol 2: Tee bilan logging
```
nmap -sS 192.168.1.0/24 | tee scan_results.txt
```
#### Misol 3: Xatoliklarni boshqarish
```
curl https://example.com &> curl.log || echo "Xatolik yuz berdi!"
```
### 6️⃣ **Rivojlangan foydalanish / Xatolarni tuzatish**
**Tinch holat (Silent Mode)**:
```
read -s -p "Parol: " pass  # Kiritishni yashirish
```
- **Kirish uchun vaqtni cheklash**:
```
read -t 10 -p "Tez! Javob (10s): " Javobi
```
- **Ko‘p chiqishli logging**:
```
cmd | tee >(grep "ERROR" > errors.log) > output.log
```
### 7️⃣ **Maslahatlar & Yashirin xatolar**
