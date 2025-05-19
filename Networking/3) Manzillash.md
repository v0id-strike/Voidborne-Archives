## Tarmoq qatlami

**OSI modeli** ning **tarmoq qatlami (3-qatlam)** ma’lumotlar paketlarini uzatishni boshqaradi, ularni to‘g‘ridan-to‘g‘ri qabul qiluvchiga jo‘natib bo‘lmaydi va shuning uchun tarmoq tugunlari orqali oraliq marshrutlashni talab qiladi. Ushbu paketlar o'z manziliga yetguncha tugundan tugunga o'tadi. Bunga erishish uchun **tarmoq qatlami** tarmoq tugunlarini aniqlaydi, ulanishlarni o'rnatadi, marshrutlash va ma'lumotlar oqimini boshqaradi. Uzatish vaqtida u manzillarni baholaydi va shunga mos ravishda tarmoq orqali paketlarni yo'naltiradi. Odatda, yuqori qatlam ma'lumotlari har bir tugunda 3-qatlam tomonidan qayta ishlanmaydi. Marshrutlash qarorlari va marshrutlash jadvalini qurish manzil ma'lumotlariga asoslanadi.

Xulosa qilib aytganda, u quyidagi vazifalarni bajaradi:
- Mantiqiy manzillash
- Marshrutlash

Har bir **OSI** qatlami ma'lum protokollardan foydalanadi - bu qatlam ichidagi aloqani boshqaradigan qoidalar to'plami. Ushbu protokollar boshqa qatlamlardan mustaqil ishlaydi, lekin ba'zilari bir nechta qatlamlarni qamrab olishi mumkin.
Tarmoq qatlami protokollariga quyidagilar kiradi:
- IPv4 / IPv6
- IPsec
- ICMP
- IGMP
- RIP
- OSPF    

Uning roli turli yoki nomuvofiq adreslash usullaridan foydalansa ham, paketlarni quyi tarmoqlar bo'ylab yoki ichida manbadan manzilga yetkazib berishni ta'minlashdan iborat. Bu butun tarmoq bo'ylab ma'lumotlarni marshrutlashni o'z ichiga oladi, marshrutizatorlar paketlarni tugun bo'yicha yo'naltiradi va ko'pincha ularga yangi oraliq maqsadlarni tayinlaydi. Ushbu yuborilgan paketlar yuqori OSI qatlamlariga etib bormaydi.

---

## IPv4 Manzillar

Tarmoqdagi har bir qurilmani mahalliy tarmoq ichida aloqa qilish imkonini beruvchi **MAC manzili** orqali aniqlash mumkin. Biroq, boshqa tarmoqdagi xostga ulanish MAC manzilidan ko'proq narsani talab qiladi - bu holatda **IPv4** yoki **IPv6** manzillari yordamga keladi. Bu manzillar tarmoq qismi va xost qismidan iborat.

Bu barcha tarmoqlar uchun amal qiladi - mahalliy uy tarmog'i yoki butun Internet. **IP manzil** ma'lumotlarning to'g'ri qabul qiluvchiga yetib borishini ta'minlaydi. Buni shunday tasavvur qilsa bo'ladi:
```
IPv4 / IPv6 - qabul qiluvchining ko'cha manzili.
MAC - ma'lum kvartira raqami.
```

IP-manzil bitta qurilmaga (unicast), bir nechta qurilmalarga (efirga uzatish) yoki bir nechta manzilga javob beradigan bitta qurilmaga tayinlanishi uchun ishlatilishi mumkin. Har bir IP-manzil o'z tarmog'ida noyob bo'lishi juda muhimdir.
### IPv4 Structure

IP-manzillar uchun standart format **IPv4** bo'lib, to'rtta 8-bitli oktetga guruhlangan 32 ikkilik bitdan iborat. Ular odam oʻqiy oladigan **nuqta-oʻnlik** formatiga aylantiriladi, har bir oktet 0 dan 255 gacha oraliqda bo'ladi.

Masalan:

| Format  | Example                             |
| ------- | ----------------------------------- |
| Binary  | 01111111.00000000.00000000.00000001 |
| Decimal | 127.0.0.1                           |

Har bir qurilma interfeysiga (masalan, kompyuterlar, marshrutizatorlar, printerlar) o'ziga xos IP-manzil beriladi.

**IPv4** 4,2 milliarddan ortiq noyob manzillarga ega. Har bir manzil tarmoq va xost qismiga bo'lingan. Uyda routerlar xost qismini tayinlaydi; tarmoq qismi provider yoki global miqyosda **IANA** tomonidan tayinlangan.
 
 **Subtarmoq niqobi**
Subtarmoqlar **pastki tarmoq maskasi** yordamida yaratiladi, bu IP-manzilning qaysi bitlari tarmoq va xostni ifodalashini aniqlaydi.

**Network and Gateway Addresses**
Har bir quyi tarmoqda ikkita qoʻshimcha zahiralangan IP **tarmoq manzili** va **efir manzili** uchun. **standart shlyuz** - odatda birinchi yoki oxirgi tayinlanadigan IP - turli tarmoqlarni ulaydi va protokollar va uzatishlarni boshqaradi.

---
## Subnetting

**Subnetting** kattaroq manzil maydonini **subnets** deb nomlangan kichikroqlarga ajratadi.

Quyi tarmoq tarmoqning barcha qurilmalari bir xil tarmoq manziliga ega bo'lgan qismidir. Bu binodagi bo'limlarni ajratish kabi tashkil etish va segmentatsiya qilish imkonini beradi.
Berilgan:
- IPv4: 192.168.12.160
- Subnet maskasi: 255.255.255.192
- CIDR: /26 

Biz **tarmoq** va **host** qismlarini aniqlash uchun ikkilik shakllarni tahlil qilamiz. Subtarmoq niqobining 1-bitlari tarmoq qismini aniqlaydi. Qolgan bitlar xostni manzillash imkonini beradi.

Agar:
- Tarmoq manzili: 192.168.12.128
- Efir manzili: 192.168.12.191
- Foydalanadigan xostlar: 192.168.12.129–192.168.12.190
- Jami foydalaniladigan xostlar: 62 (zahira uchun 64 - 2)

Buni 4 ta quyi tarmoqqa bo'lish uchun pastki tarmoq niqobini /26 dan /28 gacha oshiring (2 bit qo'shadi).

| Subnet | Tarmoq Manzili | Birinchi Host | Ohirgi Host | Efir Manzili | CIDR |
| ------ | -------------- | ------------- | ----------- | ------------ | ---- |
| 1      | 192.168.12.128 | .129          | .142        | .143         | /28  |
| 2      | 192.168.12.144 | .145          | .158        | .159         | /28  |
| 3      | 192.168.12.160 | .161          | .174        | .175         | /28  |
| 4      | 192.168.12.176 | .177          | .190        | .191         | /28  |

**Aqliy subnetting**
Faqat o'zgaruvchan oktetni aniqlash kerak. Misol uchun, 192.168.1.1/25 bilan faqat 4-okteta o'zgarishi mumkin. Xost oralig'ini topish uchun:
- /25 = 2^7 = 128 ta manzil
- Diapazon: 192.168.1.0–127 va 192.168.1.128–255 (keyingi blok) 

---

## MAC Manzil

Har bir qurilma tarmoq interfeysini identifikatsiya qiluvchi 48 bitli **MAC manzilga** ega. Standartlarga quyidagilar kiradi:
- Ethernet (IEEE 802.3)
- Bluetooth (IEEE 802.15)
- WLAN (IEEE 802.11)

Misol formatlari:
- `DE:AD:BE:EF:13:37`
- `DE-AD-BE-EF-13-37`
- `DEAD.BEEF.1337`

Dastlabki 3 bayt (OUI) ishlab chiqaruvchini aniqlaydi, oxirgi 3 bayt NICga xosdir. MAC-larni soxtalashtirish mumkin, lekin odatda apparatda o'rnatiladi.

MAC manzili funksiyalariga unicast, multicast va broadcast yetkazib berish kiradi. ARP IP-ni MAC-manzillarga hal qiladi.

**Manzilni aniqlash protokoli (ARP)**
**ARP** mahalliy aloqa uchun IP manzillarni MAC manzillariga tarjima qiladi. U translyatsiya so'rovlari va to'g'ridan-to'g'ri javoblar orqali ishlaydi.

Misol (ARP so'rovi/javob):
```
1 Kimda 10.129.12.101 bor? 10.129.12.100 ga ayting
2 10.129.12.101 AA:AA:AA:AA:AA:AA da joylashgan
```

ARP dan **spoofing** orqali foydalanish mumkin, bunda tajovuzkor o'z tizimi orqali trafikni qayta yo'naltirish uchun noto'g'ri javoblar yuboradi.

---

## IPv6 Manzil

**IPv6**, IPv4 ning vorisi, 128-bitli manzillardan foydalanadi. Afzalliklarga quyidagilar kiradi:
- Keng manzil maydoni
- Avtokonfiguratsiya (SLAAC)
- O'rnatilgan IPsec
- NAT kerak emas
- Soddalashtirilgan sarlavha
- 4 GB gacha paket hajmi

Manzil turlari:
- **Unicast**: birma-bir
- **Anycast**: birdan-yaqin
- **Multicast**: Birdan ko'pga
- (IPv6 da translyatsiya yo'q)

IPv6 o'n oltilik sanoq tizimidan foydalanadi. **prefiks** tarmoq qismini bildiradi; **interfeys identifikatori** ko'pincha MAC manzilidan olinadi.

IPv6 misoli:
- Toʻliq: `fe80:0000:0000:0000:dd80:b1a9:6687:2d3b/64`
- Siqilgan: `fe80::dd80:b1a9:6687:2d3b/64`

IPv6 notatsiyasi bo'yicha ko'rsatmalar (RFC 5952):
- Kichik harflardan foydalaning
- Boshlovchi nollarni olib tashlang
- Uzoq nol ketma-ketliklar uchun `::` dan foydalaning (faqat bir marta)
