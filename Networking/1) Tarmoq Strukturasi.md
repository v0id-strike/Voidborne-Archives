# Kirish

## **1. Tarmoq nima?**

**Tarmoq** kompyuterlarni bir-biri bilan bog'laydi.
Ular:
* Turli **shakllar** (yulduz yoki to'r kabi)
* Turli **ulanish usullari** (kabellar yoki Wi-Fi kabi)
* Turli **qoidalar** (TCP va UDP kabi protokollar deb ataladi)
dan foydlanadi.

## **2. Tarmoq qanday ishlaydi?**

* **veb-sayt manzili** (masalan, `www.hackthebox.eu`) uy manzili deb oladigan bo'lsak.
* **Router** mahalliy pochta bo‘limlariga, **ISP’lar** esa markaziy pochta xizmatiga o‘xshaydi.
* **DNS** - bu sizning xabaringizni qayerga yuborishni topadigan manzillar kitobidir. 

Internetga kirganingizda, so'rovingiz quyidagicha bo'ladi: 
**Kompyuteringiz → Router → ISP → DNS → Veb-sayt → Kompyuteringiz**
  ![net_overview](https://academy.hackthebox.com/storage/modules/34/redesigned/net_overview.png)

---

# Tarmoq Turlari

Kompyuter tarmoqlari haqida o'rganayotganda, har xil tarmoq turllari va atamalar bilan adashish oson. Ba'zilari har kuni ishlatiladi, boshqalari esa asosan darsliklarda yoki imtihonlarda paydo bo'ladi. Ushbu qoʻllanma **umumiy atamalarni** **kitob atamalaridan** ajratadi.
## **Umumiy atamalar

| **Type**                         | **What It Means**                                                              |
| -------------------------------- | ------------------------------------------------------------------------------ |
| **WAN (Keng tarmoq)**            | Ko'plab kichikroq tarmoqlarni bog'laydigan har qanday katta tarmoq. (Internet) |
| **LAN (Mahalliy tarmoq)**        | Sizning uy yoki ofis tarmog'ingiz - odatda simli.                              |
| **WLAN (Simsiz LAN)**            | Kabellar o'rniga Wi-Fi orqali ishlaydigan LAN.                                 |
| **VPN (Virtual xususiy tarmoq)** | Sizni boshqa tarmoqqa bog'laydigan xavfsiz "tunnel".                           |

### **WAN**

WAN keng tarmoq degan ma'noni anglatadi va odatda **Internet** deb ham ataladi. U ko'plab LANlarni, shaharlar, va mamlakatlarni dunyo bo'ylab birlashtiradi.

### **LAN and WLAN**

* **LAN**: Kichik hududda (uyingiz kabi) ulangan kompyuterlar guruhi. `192.168.1.x` kabi IP-lardan foydalanadi.
* **WLAN**: Kabellar o‘rniga Wi-Fi-dan foydalanadigan LAN — xuddi shu fikr, shunchaki simsiz.

Siz mehmonxonalar yoki maktablarda umumiy IP-ni olishingiz mumkin, lekin ko'pchilik uy tarmoqlari RFC1918-dan **xususiy IP diapazonlaridan** foydalanadi.
### **VPN**

VPN-lar uzoqdan turib ham tarmoqqa **xavfsiz va shaxsiy** kirishga yordam beradi. Uch tur mavjud:

* **Site-to-Site VPN**: butun tarmoqlarni bir-biriga ulaydi.
* **Remote Access VPN**: Qurilmangizga tarmoq ichidagidek harakat qilish imkonini beradi.
* **SSL VPN**: Brauzeringiz ichida ishlaydi. Ish stollari yoki ilovalarga masofadan kirish imkonini beradi.

> 🔐 **Split-Tunnel VPN'lari** VPN orqali ma'lum tarmoqlar uchun trafik yuboradi. Boshqalar odatdagidek ishlaydi. Laboratoriyada foydalanish uchun juda yaxshi, lekin kompaniyalar uchun har doim ham xavfsiz emas.
## **Kitobiy Atamalar**

| **Type**                                | **What It Means**                                                                   |
| --------------------------------------- | ----------------------------------------------------------------------------------- |
| **GAN (Global hududiy tarmoq)**         | Internet yoki kompaniyaning global tarmoqlari kabi ulkan tarmoqlar.                 |
| **MAN (Metropolitan hududiy tarmog'i)** | Bir shahar yoki mintaqada LAN tarmoqlarini ulaydi.                                  |
| **PAN/WPAN (Shaxsiy hudud tarmog'i)**   | Bir kishi atrofidagi juda kichik tarmoqlar (masalan, Bluetooth yoki USB almashish). |

### **GAN**

GANlar bir nechta WAN-larni ulaydi. Ular dengiz osti kabellari yoki sun'iy yo'ldoshlar kabi tezkor ulanishlardan foydalanadilar.

### **MAN**

MAN lar ma'lum bir **shahar yoki mintaqada** mahalliy tarmoqlarni bog'laydi. Kompaniyalar turli binolardagi ofislarni ulash uchun MANlardan foydalanadilar. Ular Internetga ulanishdan tezroq va optik tolali kabellardan foydalanadi.

### **PAN/WPAN**

PAN va WPAN - bu bitta odam yoki qurilma atrofidagi kichik tarmoqlar.
Misollar:
* **PAN**: noutbuk va telefoningiz o'rtasidagi USB kabeli ulanishi.
* **WPAN**: naushniklar, aqlli soatlar yoki IoT qurilmalari uchun Bluetooth ulanishi. 
Aqlli uylar ko'pincha chiroqlar, qulflar yoki sensorlarni boshqarish uchun ZigBee yoki Z-Wave kabi WPAN protokollaridan foydalanadi.

---

# Tarmoq Topologiyalari

Tarmoq topologiyasi kompyuter tarmog'idagi turli elementlar - tugunlar, havolalar va qurilmalarning joylashuvini anglatadi. U tarmoqdagi turli qurilmalar qanday ulanganligini va ular bir-biri bilan qanday aloqa qilishini belgilaydi. Topologiyalar tarmoqning ishlashi, kengaytirilishi, ishonchliligi va muammolarni bartaraf etish strategiyalarini aniqlashda muhim rol o'ynaydi. Ularni ikkita asosiy turga bo‘lish mumkin: **fizik topologiya**, haqiqiy fizik bog‘lanishlarni ko‘rsatuvchi va **mantiqiy topologiya**, tarmoq ichidagi ma’lumotlar oqimini ifodalaydi.

Yaxshi mo'ljallangan tarmoq topologiyasi ma'lumotlar oqimi samaradorligini oshiradi, tarmoq tiqilib qolishini kamaytiradi va yuqori mavjudlik va nosozliklarga chidamliligini ta'minlaydi.

## **Tarmoq Topologiyalarining Turlari**

### 1. **Point-to-Point Topology**

**Nuqtadan Nuqtaga** topologiyasi tarmoq konfiguratsiyasining eng oddiy shakli bo‘lib, bunda ikkita qurilma bir-biriga bevosita ulanadi. Ushbu topologiya minimal kechikish va yuqori ma'lumotlar xavfsizligini ta'minlaydigan maxsus ulanishni taklif qiladi. U ko'pincha ijaraga olingan tarmoqlarda va an'anaviy telefoniya tizimlarida qo'llaniladi. Biroq, u faqat ikkita qurilmani birlashtirgani uchun kengaytirilishi mumkin emas.

![topo_p2p](https://academy.hackthebox.com/storage/modules/34/redesigned/topo_p2p.png)

### 2. **Bus Topology**

**Avtobus Topologiyasida** barcha qurilmalar avtobus yoki magistral deb ataladigan yagona markaziy kabelga ulangan. Qurilmalar vositani ulashadi va ma'lumotlar barcha tugunlarga uzatiladi. Ma'lumotlarni faqat mo'ljallangan oluvchi qabul qiladi; boshqalar buni e'tiborsiz qoldiradilar. Ushbu topologiya tejamkor va kichik tarmoqlar uchun sodda, lekin qo'shimcha qurilmalar qo'shilganligi sababli unumdorlik bilan bog'liq muammolar mavjud. Bundan tashqari, markaziy kabeldagi nosozlik butun tarmoqni buzishi mumkin.

![topo_bus](https://academy.hackthebox.com/storage/modules/34/redesigned/topo_bus.png)

### 3. **Star Topology**

**Yulduzli topologiya** barcha qurilmalarni markaz hub, switch yoki routerga ulaydi. Ushbu markaziy qurilma ma'lumotlar trafigini boshqaradi va boshqaruvchi vazifasini bajaradi. Yulduzli topologiya o'zining mustahkamligi va muammolarni bartaraf etish qulayligi tufayli zamonaviy LANlarda keng qo'llaniladi. Agar bitta kabel ishlamay qolsa, faqatgina o'sha kabelga ulangan qurilmaga ta'sir qiladi. Biroq, agar markaziy hub ishlamay qolsa, butun tarmoq ishlamay qoladi.

![topo_star](https://academy.hackthebox.com/storage/modules/34/redesigned/topo_star.png)

### 4. **Ring Topology**

**Halqali topologiyada** har bir qurilma aylana ma’lumotlar yo‘lini tashkil qilib, aynan ikkita boshqa qurilmaga ulanadi. Ma'lumotlar bir yo'nalishda (yoki ba'zan ikki tomonlama tarmoqlarda ikki tomonlama) tarqaladi. Token uzatish ko'pincha tarmoq muhitiga kirishni boshqarish uchun ishlatiladi. Ushbu topologiya ma'lumotlar to'qnashuvidan qochadi va tartibli uzatilishini ta'minlasa-da, agar ortiqcha halqa mavjud bo'lmasa, bitta nosozlik nuqtasi aloqani buzishi mumkin.

![topo_ring](https://academy.hackthebox.com/storage/modules/34/redesigned/topo_ring.png)

### 5. **Mesh Topology**

**To'r topologiyasi** har bir qurilmani boshqa barcha qurilmaga ulash orqali nosozliklarga chidamliligini taʼminlaydi. **To'liq To'r** da har bir tugun boshqa barcha tugunlarga ajratilgan havolaga ega. **Qisman To'r** da ba'zi tugunlar to'liq bog'langan, boshqalari esa faqat bir nechta tugunlarga ulangan. To'r topologiyalari ishonchliligi muhim bo'lgan tarmoqlar uchun ideal, masalan, WAN yoki muhim infratuzilma tizimlarida. Biroq, zarur bo'lgan ko'p sonli ulanishlar tufayli ulardan foydalanish qimmat va murakkab.

![topo_mesh](https://academy.hackthebox.com/storage/modules/34/redesigned/topo_mesh.png)

### 6. **Tree Topology**

**Daraxt topologiyasi** yulduz va avtobus topologiyalarining xususiyatlarini birlashtirgan tuzilmadir. U chiziqli avtobus magistraliga ulangan yulduzcha konfiguratsiya qilingan tarmoqlar guruhlaridan iborat. Ushbu tuzilma keng ko'lamli va turli bo'limlari yoki qavatlari bo'lgan yirik tashkilotlar uchun juda mos keladi. Biroq, asosiy yo'nalishdagi nosozlik butun tarmoqqa ta'sir qilishi mumkin.

![topo_tree](https://academy.hackthebox.com/storage/modules/34/redesigned/topo_tree.png)

### 7. **Hybrid Topology**

**gibrid topologiya** ikki yoki undan ortiq turli turdagi topologiyalarning individual afzalliklarini birlashtiradi. Masalan, kompaniya bo'limlar ichida yulduz topologiyasidan foydalanishi va ularni daraxt topologiyasini shakllantirgan holda avtobus magistralidan foydalanib ulashi mumkin. Gibrid tarmoqlar moslashuvchanlik, va ishlashni optimallashtiradi, ammo loyihalash va boshqarish uchun murakkab.

![topo_hybrid](https://academy.hackthebox.com/storage/modules/34/redesigned/topo_hybrid.png)

### 8. **Daisy Chain Topology**

**Daisy zanjir topologiyasida** qurilmalar birin-ketin chiziqli ketma-ket ulanadi. Kichik o'lchamli tarmoqlar uchun sodda va tejamkor bo'lsa-da, bu topologiya jiddiy cheklovlarga ega: agar bitta qurilma ishlamay qolsa, quyi oqim qurilmalari ulanishni yo'qotadi. Sanoat avtomatizatsiyasidan tashqari zamonaviy tarmoqlarda kamdan-kam qo'llaniladi.

![topo_daisy-chain](https://academy.hackthebox.com/storage/modules/34/redesigned/topo_daisy-chain.png)
 
  --- 
 
# Proksi-serverlar

## **Proksi nima?**

**proksi-server** mijoz (masalan, kompyuter yoki brauzer) va server (masalan, veb-sayt) o'rtasida vositachi vazifasini bajaradi. To'g'ridan-to'g'ri manbaga ulanish o'rniga, mijoz o'z so'rovini proksi-serverga yuboradi, so'ngra mijoz nomidan so'rovni yo'naltiradi. Javob olingandan so'ng, proksi-server mijozga ma'lumotni qaytaradi.

**"proksi"** so'zining o'zi "nomidan" degan ma'noni anglatadi, bu uning funktsiyasini mukammal tavsiflaydi: proksi-server foydalanuvchi nomidan ishlaydi.

## **Nima uchun proksi-serverdan foydalanish kerak?**

Proksi-serverlar turli sohalarda va foydalanuvchi ehtiyojlariga qarab ko'p maqsadlarga xizmat qiladi:

* **Xavfsizlik**: zararli harakatlar uchun trafikni filtrlash yoki kuzatish.
* **Maxfiylik**: mijozning IP manzilini yashirish uchun.
* **Kirish nazorati**: Muayyan veb-saytlar yoki xizmatlarni bloklash yoki ruxsat berish.
* **Ishlash**: Ma'lumotlarni keshlash va tarmoq kechikishini kamaytirish uchun.
* **Test**: nosozliklarni tuzatish uchun tarmoq trafigini ushlab turish va o‘zgartirish (masalan, kiberxavfsizlikda Burp Suite).

## **Proksi turlari**

Proksi-serverlarning bir nechta turlari mavjud, ularning har biri o'ziga xos rollari va foydalanish holatlariga ega. Eng muhimlari quyidagilardir:

### 1. **O'tkazish proksi (maxsus proksi)**

O'tkazish proksi-serveri mijoz va server o'rtasida joylashgan. U ichki foydalanuvchilarning so'rovlarini qabul qiladi va ularni tashqi manbalarga yuboradi. Tashkilotlar ko'pincha quyidagi maqsadlarda proksi-serverlardan foydalanadilar:

* Internetdan foydalanish qoidalarini qo'llash.
* Veb-faoliyatni kuzatib borish va qayd qilish.
* Ba'zi saytlarga kirish huquqini cheklash.

![forward_proxy](https://academy.hackthebox.com/storage/modules/34/redesigned/forward_proxy.png)

### 2. **Teskari proksi**

O'tkazish proksi-serverdan farqli o'laroq, teskari proksi-server server oldida turib, Internetdagi mijozlarning so'rovlarini serverga yetib borishidan oldin ushlab ushlab qoladi. Odatda quyidagilar uchun ishlatiladi:

* Bir nechta serverlarda yuklarni muvozanatlash.
* Ichki serverlarni bevosita ta'sir qilishdan himoya qilish.
* Veb-ilovalar xavfsizlik devori (WAF) sifatida ishlaydi.

**Misol**: Cloudflare kabi xizmatlar veb-saytlarni DDoS hujumlari va zararli foydalanuvchilardan himoya qilish uchun teskari proksi sifatida ishlaydi.

![reverse_proxy](https://academy.hackthebox.com/storage/modules/34/redesigned/reverse_proxy.png)

### 3. **Shaffof proksi**

Shaffof proksi mijoz tomonida hech qanday konfiguratsiyani talab qilmasdan trafikni filtrlaydi. Foydalanuvchilar ko'pincha proksi-serverning orqasida ekanliklarini anglamaydilar. Ular odatda umumiy Wi-Fi yoki ta'lim muhitlarida kirishni kuzatish yoki cheklash uchun ishlatiladi.

**Misol**: Maktab va Universitetlar hech qanday qurilma sozlamalarini o‘zgartirmagan holda o‘quvchilar uchun ma’lum veb-saytlarni bloklash uchun shaffof proksi-serverdan foydalanadi.

## **Proksi va VPN**

Ko'p odamlar proksi-serverlarni VPN bilan chalkashtirib yuborishadi. Ikkalasi ham IP manzilingizni yashirishi va maxfiylikni taminlasa-da, ular boshqacha ishlaydi:

* **proksi** odatda **dastur qatlamida** (OSI modelining 7-qatlami) ishlaydi va brauzer kabi muayyan dasturiy ta'minotga ta'sir qiladi.
* **VPN** ** tarmoq qatlamida ishlaydi, u nafaqat veb-so'rovlarni, balki qurilmadan barcha trafikni shifrlaydi.

Qisqacha qilib aytganda, VPN-lar xavfsizroq, lekin ayni paytda ko'proq resurs talab qiladi, proksi-serverlar esa engil va maxsus foydalanish holatlariga xizmat qiladi.

## **Kiberxavfsizlikda proksi-serverlar**

Kiberxavfsizlikda proksi-serverlar kuchli vositadir:

* **Burp Suite** brauzer va veb-server o'rtasidagi HTTP trafigini ushlab turish va o'zgartirish uchun ishlatiladi.
* **SOCKS yoki SSH proksi-serverlari** Red Teamerlar yoki testerlarga tarmoqlar ichida “pivot” qilish va ulanib bo'lmaydigan tizimlarga boshqa yo'l bilan bog'lanish imkonini beradi.
* **Viruslar** proksi-server sozlamalariga moslashish orqali filtrlash tizimlarini chetlab o'tishi mumkin.

Proksi-serverlar qanday ishlashini tushunish himoyachilarga yaxshiroq boshqaruvni o'rnatishga va Red-Teamerlarga zaif tomonlarni tekshirishga yordam beradi.

