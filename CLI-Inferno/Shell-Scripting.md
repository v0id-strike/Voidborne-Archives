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
- ✅ **Har doim o‘zgaruvchilarni boshlang‘ich qiymat bilan to‘ldiring**:
```
declare -i hosts_up=0  # Sanoq uchun butun son
```
- ❌ **Logs fayllarini yozib yuborish**: Muhim ma'lumotlar uchun `>>` yoki `tee -a` ishlating.
- ✅ **Kirishni tekshirish**:
```
[[ "$opt" =~ ^[1-3]$ ]] || exit 1
```
### 8️⃣ **Xulosa**
> Asosiy xulosalar:
> - Interaktiv menyular uchun `read` + `case`ni ishlating.
> - Real vaqtda monitoring va logging uchun `tee` juda yaxshi.
> - Xatoliklarni (`2>`) yordamida alohida faylga yo‘naltiring.
> - Kirish tekshiruvining barcha chekka holatlarini sinab ko‘ring.
### 🔖 Bonus: Pro maslahatlar
- **Menyu so‘rovlari rang bilan bezash**:
```
echo -e "\e[32m1) Skanerlash\e[0m"  # Yashil matn
```
- **Audit trail (audit izlari)**:
```
echo "$(date): Foydalanuvchi $opt tanladi" >> audit.log
```
## 📌 8-faza: Oqimni boshqarish va sikllar
### 1️⃣ **Kirish / Ta’rif**
> Bash’dagi oqimni boshqarish tuzilmalari skript buyruqlarining shartlar va takrorlanishga asoslangan bajarilishini boshqaradi. Ular quyidagilarni ta’minlaydi:
> - **Qaror qabul qilish** (`if`, `case`)
> - **Takroriy bajarish**** (`for`, `while`, `until`)
> - **Chiqishni boshqarish** (`tee`, yo‘naltirish)
### 2️⃣ **Sintaksis bloki**
#### Shoxlanish:
```
# If-Else
if [ "$var" -eq 1 ]; then  
    komandalar  
elif [ "$var" -eq 2 ]; then  
    komandalar  
else  
    komandalar  
fi  

# Case
case $var in  
    "a") komandalar ;;  
    "b") komandalar ;;  
    *) standart_komandalar ;;  
esac  
```
#### Sikllar:
```
# For
for item in {1..5}; do  
    komandalar  
done  

# While
while [ $counter -le 5 ]; do  
    komandalar  
    ((counter++))  
done  

# Until
until [ $counter -gt 5 ]; do  
    komandalar  
    ((counter++))  
done  
```
#### Chiqishni boshqarish:
```
command | tee file.txt          # Terminalga chiqarish + faylga saqlash  
command >> file.txt 2>&1        # stdout/stderr’ni faylga qo‘shish  
```
### 3️⃣ **Sintaksis izohi**
- ✅ `if [ ]` → `[ ]` ichida bo‘shliqlar majburiy. Raqamlar uchun `-eq`, satrlar uchun `==` ishlatiladi.
- ✅ `case` → Bir nechta holatlarni aniqlash uchun `if`ga nisbatan soddaroq. Har bir holatni `;;` bilan tugating.
- ✅ `for` → Ro‘yxatlar bo‘yicha aylanadi (`{1..5}`, `*.txt`, `${array[@]}`).
- ✅ `while` / `until` → Cheksiz sikldan saqlanish uchun o‘zgaruvchilarni yangilashni unutmang.
- ❌ **Iqtibossiz o‘zgaruvchilar** → So‘zlarni noto‘g‘ri bo‘lishi mumkin (`[ ]`) testlarida muammo.
### 4️⃣ **Qachon / Nega ishlatiladi?**
| Vaziyat                              | Tuzilma           | Misol                      |                 |
| ------------------------------------ | ----------------- | -------------------------- | --------------- |
| Menyu asosidagi skriptlar            | `case`            | `CIDR.sh` opsiyalar        |                 |
| Fayllar yoki IP’lar bo‘yicha aylanis | `for`             | `for ip in $(prips $cidr)` |                 |
| Xatolarga chidamli bajarish          | `while` + `break` | Xatolikda qayta urinish    |                 |
| Real vaqtda loglash                  | `tee`             | scan                       | tee -a log.txt` |
### 5️⃣ **Misollar**
#### Misol 1: Tarmoq skaneri
```
for ip in $(prips 192.168.1.0/24); do  
    ping -c 1 $ip >/dev/null && echo "$ip: LIVE" | tee -a live_hosts.txt  
done
```
#### Misol 2: Foydalanuvchi menyusi
```
case $choice in  
    1) nmap -sV $target ;;  
    2) ping -c 4 $target ;;  
    3) exit 0 ;;  
    *) echo "Noto‘g‘ri tanlov" && exit 1 ;;  
esac
```
#### Misol 3: Faylni shartli qayta ishlash
```
while read -r file; do  
    if [ -f "$file" ]; then  
        wc -l "$file"  
    else  
        echo "Yo‘q: $file" >> errors.log  
    fi  
done < file_list.txt
```
### 6️⃣ Kengaytirilgan foydalanish / Hiylalar
- **Siklni nazorat qilish:**
```
for i in {1..100}; do  
    [ $i -eq 50 ] && break     # Erta chiqish  
    [ $i -lt 10 ] && continue  # Ba’zi aylanishlarni o‘tkazib yuborish  
done
```
- **Fon rejimida ishlash**:
```
while read ip; do  
    ping $ip &  # Har bir ping’ni fon rejimida bajarish  
done < ips.txt
```
- **Tee uchun nomlangan quvurlar (pipe)**:
```
mkfifo pipe  
command | tee pipe > output.log &  
grep "ERROR" pipe > errors.log
```
### 7️⃣ **Maslahatlar va xatolar**
- ✅ **O‘zgaruvchilarni iqtibosga oling**: `[ "$file" = "test" ]` (bo'sh joylar bilan xavfsiz ishlaydi).
- ❌ **Cheksiz aylanishlar (infinite loops)** : Aylanishdagi o'zgaruvchilarni doimo yangilab boring (`((i++))`).
- ✅ **Regex uchun `[[ ]]` dan foydalaning**: `[[ "$str" =~ ^[0-9]+$ ]]`.
- ❌ **Faylni ustiga yozib yuborish (overwrite)**: Loglar uchun `>>` yoki tee `-a` dan foydalanish afzal.
### 8️⃣ **Xulosa**
> 🔑 Asosiy xulosalar:
> - if / case — qaror qabul qilish uchun.
> - for, while, until — takrorlovchi vazifalar uchun.
> - tee — real vaqtli ko‘rinish va loglash uchun.
> - Kirishlarni har doim tekshiring, chiqish shartlarini belgilang.
### 🔖 Bonus: Professional maslahatlar
- **Parallel bajarish**:
```
for ip in ${ips[@]}; do  
    (ping -c 1 $ip | tee -a ping.log) &  
done  
wait  # Barcha fon jarayonlarini kutish
```
- **Rangli chiqish**:
```
echo -e "\e[31mXATO\e[0m"  # Qizil matn
```
---
## **📌 9-faza: case operatorlari**
### 1️⃣ **Kirish / Ta’rif**
>   case operatorlari (ya’ni, switch-case) `if-elif-else` zanjirlariga qaraganda ancha soddaroq va toza ko‘rinishda turuvchi yozuvlarni taqdim etadi. Ular quyidagi holatlarda foydalidir:
> - **Aniq qiymat**lar bilan solishtirishda (oraliklar yoki shartlar emas).
> - **Bir nechta belgilangan variantlar** (masalan, menyular) bilan ishlaganda.
> - **Andoza**larga moslashtirishda (wildcardlar, regex-ga o‘xshash yozuvlar).

`if-else` dan asosiy farqlari: 
✅ Aniq qiymatlar uchun toza sintaksis
❌ Boolean ifodalarni (`-gt, -lt`) tekshira olmaydi
### 2️⃣ **Sintaksis Blok**
#### Asosiy tuzilma:
```
case $variable in
    pattern1)
        buyruklar
        ;;
    pattern2|pattern3)
        buyruklar
        ;;
    *)
        standart_buymruklar
        ;;
esac
```
#### CIDR.sh misoli:
```
case $opt in
    "1") network_range ;;
    "2") ping_host ;;
    "3") network_range && ping_host ;;
    "*") exit 0 ;;
esac
```
3️⃣ Sintaksis tushuntirishi
- ✅ `case $var in` → `$var` qiymatiga qarab taqqoslashni boshlaydi
- ✅ pattern) → To‘g‘ri keladigan qiymat yoki shablon:

  - `"1"` → literal `1`

  - `"*"` → barcha holatlar uchun (default case)

  - `[Yy]*` → `"Yes"`, `"yes"` kabi qiymatlar uchun mos keladi
- ✅ `;;` → Har bir blokni yakunlaydi (C tilidagi `break`ga o‘xshaydi)
- ✅ `esac` → `case` operatorini tugatadi (case teskari yozuvi)
### 4️⃣ **Qachon va nima uchun ishlatiladi**
| Holat                            | 	case yoki if?          | Misol                       |                 |
| -------------------------------- | ------------------------- | --------------------------- | --------------- |
| Menyuli skriplar                 | ✅ `case` orqali soddaroq | CIDR.sh variantlari         |                 |
| Aniq qiymatlar bilan ishlash     | ✅ `case` aniqroq         | 	`"yes" / "no"`          |                 |
| Pattern / wildcard bilan ishlash | ✅ `case` o‘zida mavjud   | `[Yy]*` — ha degan javoblar |                 |
| Sonlar oralig‘i                  | ❌ `if` kerak             | `[ $num -gt 10 ]`           | tee -a log.txt` |
 ### 5️⃣ **Misollar**
#### 1-misol: Oddiy menyu
```
read -p "Amal (start|stop|restart): " cmd
case $cmd in
    "start") systemctl start nginx ;;
    "stop") systemctl stop nginx ;;
    "restart") systemctl restart nginx ;;
    *) echo "Noto‘g‘ri buyruq" && exit 1 ;;
esac
```
#### 2-misol: Wildcard moslik
```
read -p "Tasdiqlang (Y/n): " answer
case $answer in
    [Yy]*) echo "Davom etamiz..." ;;
    [Nn]*) echo "Bekor qilindi." && exit 0 ;;
    *) echo "Noto‘g‘ri kiritma" ;;
esac
```
#### 3-misol: Ko‘p shablonli moslik
```
case $file_ext in
    "jpg"|"png"|"gif") echo "Rasm fayli" ;;
    "txt"|"md") echo "Matn fayli" ;;
    "sh") echo "Skript fayli" ;;
esac
```
### 6️⃣ **Kengaytirilgan ishlatish / Foydali usullar**
- **Regexga o‘xshash shablonlar**:
```
case $host in
    web*) echo "Veb server" ;;        # "web" bilan boshlanadi
    *db) echo "Ma’lumotlar bazasi" ;; # "db" bilan tugaydi
esac
```
- **Bir nechta holatni ketma-ket bajarish (Bash 4+)**:
```
;&  # Keyingi blokka o‘tadi (;; o‘rniga)
```
- **Chiqarish kodlari bilan ishlash**:
```
case $(curl -s example.com) in
    *"200 OK"*) exit 0 ;;
    *) exit 1 ;;
esac
```
### 7️⃣ **Foydali maslahatlar va xatolar**
- ✅ **Andozalarni (patterns) qo‘shtirnoqqa oling**: `"pattern"` — globbing (yulduzcha bilan moslashish) ni oldini olish uchun.
- ❌ **`;;` ni unutish**: Bu holat keyingi holatlarga "o‘tish"ga sabab bo‘ladi (ko‘pincha bu kutilmagan natijani beradi).
- ✅ **Oxirida `*` dan foydalaning**: Standart (default) holat doimo oxirgi andoza bo‘lishi kerak.
- ❌ **Ortacha chuqurlikdagi ichma-ichlik (over-nesting)**: Murakkab mantiqlardan qoching; buning o‘rniga funksiyalardan foydalaning.
### 8️⃣ **Xulosa**
> case operatori quyidagilarda juda qulay:
> - **Menyu tizimlari** ( `if-elif` dan ko‘ra ancha toza va tartibli)
> - **Aniq yoki andozaga mos tushish** (wildcardlar, `|` bilan "YOKI" holatlari)
> - **Standart holatlar** (`*` orqali)
Raqamli oraliqlar yoki mantiqiy (boolean) ifodalar uchun qulay emas.
### 🔖 Bonus: Pro Maslahatlar
- **Rangli menyular**:
```
echo -e "1) \e[32mSkanirovka\e[0m\n2) \e[31mChiqish\e[0m"
```
- **Audit log yuritish**:
```
case $opt in
    "1") echo "$(date): Skanirovka tanlandi" >> audit.log ;;
esac
```
## **📌 10-faza: function (Funktsiyalar)**
### 1️⃣ **Kirish / Ta’rif**
> Bash’dagi funksiyalar quyidagilarni ta’minlaydi:
> - **Kodni qayta ishlatish** (takrorlanishdan qochish)
> - **Yaxshi tuzilganlik** (modullashtirilgan tuzilma)
> - **Mahalliy o‘zgaruvchilar** ( local kalit so‘zi bilan )
> - **Parametrlar uzatish** ($1, $2 — funksiyada foydalaniladi)
> - **Qaytariladigan qiymatlar** ( exit code yoki stdout orqali)
### 2️⃣ **Sintaksis Bloki**
#### Funksiya yaratish:
```
# 1-usul (aniq)
function nomi {
    buyruklar
}

# 2-usul (ixcham)
nomi() {
    buyruklar
}
```
#### Funksiyani chaqirish:
```
nomi              # Argumentlarsiz
nomi "arg1"       # Argument bilan
```
#### Qiymatni qaytarish:
```
return 0          # Muvaffaqiyat (0-255 oraliqda)
echo "qiymat"     # Chiqishni ushlash uchun
```
### 3️⃣ **Sintaksis izohi**
- ✅ **`function` kalit so‘zi**: Majburiy emas, lekin o‘qilishi osonroq qiladi
- ✅ **Parametrlar**: `$1`, `$2` orqali olinadi (funksiya doirasida)
- ✅ **`local` o‘zgaruvchilar**: Ko‘lamni cheklaydi: `local var="qiymat`".
- ❌ **Standart holatda global**: E’lon qilinmagan o‘zgaruvchilar butun skriptga ta’sir qiladi.
### 4️⃣ **Qachon va nima uchun ishlatiladi**
| Holat           | Funksiya afzalligi            | Misol                            |
| --------------- | ----------------------------- | -------------------------------- |
| Takroriy kod	  | Bitta ta’rif, ko‘p chaqirish  | `network_range()` `CIDR.sh` da   |
| Murakkab mantiq | Alohida tekshirish, tuzatish  | Kiritilgan ma’lumotni tekshirish |
| Skriptni tuzish | Mantiqiy bo‘limlarga ajratish | `main()` with sub-functions      |
5️⃣ Misollar
#### 1-misol: Oddiy funksiya
```
function salomlash {
    echo "Salom, $1!"
}
salomlash "Ozodbek"  # → "Salom, Ozodbek!"
```
#### 2-misol: Status (kod) qaytarish
```
function fayl_bormi {
    [ -f "$1" ] && return 0 || return 1
}
fayl_bormi "test.txt"
echo "Mavjudmi? $?"  # 0=ha, 1=yo‘q
```
#### 3-misol: Chiqishni ushlash
```
function ip_ol {
    host $1 | grep "has address" | cut -d" " -f4
}
iplar=$(ip_ol "example.com")
```
### 6️⃣ **Kengaytirilgan foydalanish / Foydali usullar**
- **Dinamik o‘zgaruvchilar**:
```
function o_rnat {
    local "$1"="$2"  # Xavfsiz tayinlash
}
o_rnat "rang" "qizil"
```
- **Array (ro‘yxat) argumentlari**:
```
function fayllarni_kor {
    for file in "$@"; do
        wc -l "$file"
    done
}
fayllarni_kor *.txt
```
- **Xatolikni tuzatuvchi funksiya**:
```
function xavfsiz_ochir {
    [ -e "$1" ] || { echo "Fayl topilmadi"; return 1; }
    rm "$1"
}
```
### 7️⃣ **Maslahatlar va xatoliklar**
- ✅ **Har doim `local`**: Yon ta’sirlarning oldini oladi: `local counter=0`.
- ❌ **Global o‘zgaruvchilardan haddan tashqari foydalanish**: Xatoliklarni tuzatishni qiyinlashtiradi.
- ✅ **Funksiyalarni hujjatlashtiring (izoh bilan tushuntiring)**: bu kodni tushunishni va qo‘llab-quvvatlashni osonlashtiradi.
```
# Foydalanish: salomlash <ism>
# Qaytaradi: Salom matni
function salomlash { ... }
```
- ❌ **Natijani e'tiborsiz qoldirish**: `$?` orqali chiqish kodini tekshiring yoki chiqishni o‘zgaruvchiga yozib oling.
### 8️⃣ ***Xulosa**
### Asosiy xulosalar:

- Qayta ishlatiladigan kod bloklari uchun funksiyalardan foydalaning.
- `local` o‘zgaruvchilar tasodifiy global o‘zgarishlarning oldini oladi.
- Natijani `exit` kodlari orqali ( `0` = muvaffaqiyat) yoki `stdout` chiqishini ushlab olish orqali qaytaring.
- Maqsad va foydalanishni hujjatlashtiring — texnik xizmat ko‘rsatishni yengillashtiradi.
## 🔖 Bonus: Pro Maslahatlar
### Nosozliklarni aniqlash:
```
function debug {
    echo "DEBUG: $*" >&2  # stderrga chiqarish
}
debug "O‘zgaruvchi x=$x"
```
### Rangli ogohlantirish:
```
function ogohlantir {
    echo -e "\e[33mOGOH: $*\e[0m" >&2
}
ogohlantir "Diskda joy kam"
```
# 11-bosqich: Nosozliklarni tuzatish (Debugging)

## 1️⃣ Kirish / Ta’rif

Bash skriptlarida nosozliklarni tuzatish quyidagilarni aniqlash va bartaraf etishni o‘z ichiga oladi:

- **Sintaksis xatolari** (yetishmayotgan qo‘shtirnoq, qavslar)
- **Mantiqiy xatolar** (noto‘g‘ri shart yoki hisob-kitoblar)
- **Ish vaqtidagi muammolar** (ruxsatlar, yo‘q fayllar)

Asosiy vositalar: `-x` (xtrace) va `-v` (verbose) flaglari

---

## 2️⃣ Sintaksis Blogi

### Nosozliklarni tuzatish buyruqlari:

```bash
bash -x script.sh     # Qadam-baqadam bajarishni ko‘rsatadi
bash -v script.sh     # Skriptni asl holida va natijasi bilan ko‘rsatadi
bash -xv script.sh    # Har ikkisini birlashtirib, batafsil tahlil qiladi
```
### Skript ichida debugging:
```
#!/bin/bash
set -x        # Shu nuqtadan debugging yoqiladi
code_block
set +x        # Debugging o‘chiriladi
```
### 3️⃣ Sintaksis izohi
- ✅ -x → Buyruqlarni kengaytirilgan o‘zgaruvchilar/argumentlar bilan chop etadi (+ bilan ko‘rsatiladi).
- ✅ -v → Buyruqlar bajarilishidan oldin ularning asl shaklini ko‘rsatadi.
- ✅ set -x/+x → Skript ichida debugging rejimini yoqish/o‘chirish imkonini beradi.
- ❌ Breakpointlar yo‘q: IDE'lardagi kabi to‘xtatish yoki tekshirish imkoniyati Bash'da mavjud emas.
## 3️⃣ Sintaksis izohi
- ✅ `-x` → Kengaytirilgan o‘zgaruvchilar/argumentlar bilan buyruqlarni chiqaradi (`+` bilan ko‘rsatiladi).
- ✅ `-v` → Buyruqlar bajarilishidan oldin ularning asl shaklini ko‘rsatadi.
- ✅ `set -x/+x` → Skript bo‘limlarida debugging rejimini yoqish/o‘chirish imkonini beradi.
- ❌ **Breakpointlar yo‘q**: IDE dasturlaridagidek to‘xtatish yoki tekshirish imkoniyati mavjud emas.
---
## 4️⃣ Qachon va nima uchun ishlatiladi

| Holat                             | Vosita        | Misol                                            |
|-----------------------------------|---------------|--------------------------------------------------|
| O‘zgaruvchi qiymatlarini kuzatish | `-x`          | CIDR.sh ichida `$domain` o‘zgaruvchisini ko‘rish |
| Boshqaruv oqimini tekshirish      | `-x`          | `if-else` bloklarining ishlaganini tasdiqlash    |
| Skript tahlilini tekshirish       | `-v`          | Kutilmagan o‘zgaruvchilarni erta aniqlash        |
| Muammo bor kodni ajratib olish    | `set -x` blok | Faqat bitta funksiyani debugging qilish          |

---
## 5️⃣ Misollar
### Misol 1: Oddiy debugging
```bash
$ bash -x CIDR.sh inlanefreight.com
+ '[' 1 -eq 0 ']'
+ domain=inlanefreight.com
+ echo -e 'Discovered IP address:\n165.22.119.202'
Discovered IP address:
165.22.119.202
```
#### 2️⃣ Misol: Diqqatni jamlash orqali xatolikni tuzatish.
```
#!/bin/bash
# ... odatiy kodlar ...

set -x             # Debug rejimni yoqish
network_range      # Tekshirilayotgan funksiya
set +x             # Debug rejimni o‘chirish

# ... qolgan skript ...
```
#### 3️⃣ Misol: Batafsil (Verbose) rejim.
```
$ bash -v script.sh
```
```
#!/bin/bash
# Argumentlarni tekshirish
if [ $# -eq 0 ]
then
    echo "Xato: Argumentlar yo‘q"
fi
```
### 6️⃣ **Ilg‘or foydalanish / Xususiyatlar**
- **PS4 Maxsus sozlash**:  
```bash
  export PS4='+ ${BASH_SOURCE}:${LINENO}: '  # Fayl/qatordagi raqamlarni ko‘rsatish
  bash -x script.sh
```
#### Log faylga yozish:
```
bash -x script.sh 2> debug.log
```
#### Xatolikni ushlash (`trap` bilan):
```
trap 'echo "Xato $LINENO-qatorida"' ERR
```
### 7️⃣ **Maslahatlar va Ommaviy Xatoliklar**
- ✅ **Kichik boshlang**: Har safar bitta funksiya/blokni tekshirib chiqing.  
- ❌ **Ortga izlash**: Katta skriptlar uchun `-xv` dan qoching (faqat zarur bo'lganda ishlating).  
- ✅ **Toza chiqish**: Kerak bo'lganda shovqinni yo'naltiring (`2>/dev/null`).  
- ❌ **Chiqarish kodlarini e'tiborsiz qoldirish**: Muammoli buyruqlardan keyin doimo `$?` ni tekshiring.  
# Xulosa
Samarali debaglash uchun:
- `-x` - bajarilayotgan qadamlar ro‘yxati  
- `-v` - skriptni bajarishdan oldin tekshirish  
- `set -x` / `set +x` - muammoni izolyatsiya qilish  
- `echo` lar orqali mantiqni sinash  
---
## Bonus: Pro Maslahatlar
#### Rangli debag chiziqlari:  
```bash  
export PS4='\e[33m+ ${BASH_SOURCE}:${LINENO}:'\e[0m '  
bash -x script.sh 
``` 
#### Funksiya bajarilish vaqtini o‘lchash:
```
set -x; start=$SECONDS; network_range; echo "Took $((SECONDS-start))s"; set +x 
```