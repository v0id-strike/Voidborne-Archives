# Bash-da Case Statements

## Nima bu?
Case statements – Bashda o'zgaruvchi qiymatiga asoslanib oqimni boshqarish usulidir. Bu C/C++ tillaridagi switch-case konstruktsiyasiga o'xshash.

## Sintaksis
```bash
case <o'zgaruvchi> in
    pattern1 )
        buyruqlar
        ;;
    pattern2 )
        buyruqlar
        ;;
    * )
        standart buyruqlar
        ;;
esac
```
### 4. **Sintaksisning Tushuntirish**
- Har bir qismni qatorma-qator tushuntiring.
- Aniqroq bo'lishi uchun balli yoki ✅ belgilardan foydalaning.
-Misol:
  - ✅ `case <o'zgaruvchi> in` — case bayonotini boshlaydi.
  - ✅ `pattern )` — qiymatni moslashtiradi.
  - ✅ `;;` — case blokining tugashi.
  - ✅ `esac` — butun bayonotni tugatadi.
### 5. **Qachon va Nima Uchun Foydalanish**
- Foydalanish holatlarini tushuntiring.
- Ixtiyoriy: taqqoslash jadvali (agar foydali bo'lsa).
- Misol:
> *Agar sizda aniq moslamalar yoki naqshlar asosida bir nechta tanlov bo'lsa, ishlating. Ko'proq if-else yordamida boshqarishdan osonroq.*

| `Vaziyat`            | `if`               | `case`   |
| ------------------ | ------------------ | -------- |
| Raqamli taqqoslash | ✅                 | ❌       |
| Menyu variantlari	 | ✅ (lekin chalkash)| ✅ (toza)|
## 6. Misollar (Namunalar)
- Bir nechta ishlaydigan misollarni taqdim eting.
- Oddiydan boshlang, keyin murakkabgacha o'ting.
- Misol:
```bash
read -p "Enter choice: " choice
case $choice in
    1 ) echo "Option 1 selected" ;;
    2 ) echo "Option 2 selected" ;;
    * ) echo "Invalid option" ;;
esac
```
# 7. Qo‘shimcha Foydalanish / Hiylalar (Ixtiyoriy)

- Naqshlarni solishtirish, tsikllar va boshqalarni qo‘shing.
- Misol: `[Yy]` bilan naqshlarni solishtirish.

# 8. Maslahatlar va Keng Tarqalgan Xatolar

- Ixtiyoriy, lekin juda foydali.
- Tuzoqlarni eslab qolishga yordam beradi.
- Misol:  
  > Blok oxirida `;;` ni unutish xatolarga olib keladi. Har doim `esac` bilan `case` ni yoping.

# 9. Xulosa

- O‘rganilgan narsalarning tezkor takrori.
- Misol:  
  > `Case` gaplar o‘zgaruvchini naqshlar bilan solishtirib, oqimni boshqarishga yordam beradi. Ular aniq va foydalanuvchi menyulari uchun yaxshi.

# 10. Ixtiyoriy: Mashqlar / Vazifalar

- Amaliyot uchun narsalarni ro‘yxatlang.
- Misol:  
  > 3 ta menyu varianti bo‘lgan skript yarating.  
  > `[A-Za-z]` bilan naqshlarni solishtirishni sinab ko‘ring.  
  > Tsikl ichida `case` gapini yarating.
### 🔖 Bonus  
Agar siz raqamli eslatmalarni olib borayotgan bo'lsangiz, shuningdek quyidagilarni ham ishlatishingiz mumkin:
- ✅ Tez navigatsiya uchun sarlavhalardan foydalaning.  
- ✅ Vazifalar uchun tekshirish ro'yxatlarini foydalaning.  
- ✅ Tushunarli bo'lishi uchun kod bloklaridan foydalaning.  
- ✅ Vizual esda qolish uchun emoji yoki ikonkalardan foydalaning (masalan, ✅, ❌, 🧩, 🚀).
### 📂 Namuna Vizual Tartib
---
```
# Bash-da Case Statements
## Nima bu?  
Tezkor tushuntirish...
## Sintaksis  
(case blok)
## Tushuntirish  
- `case <o'zgaruvchi> in` — ...
- `pattern )` — ...

## Qachon Ishlatish  
| Vaziyat                | if | case |
...
## Misollar  
( kod misoli )

## Maslahatlar va Xatolar  
- ✅ `;;` ni eslab qoling.  
- ❌ `esac` ni unutmaslikka harakat qiling.

## Xulosa  
Tezkor xulosa...

## Mashqlar  
- [ ] Menyu skriptini yaratish.
```