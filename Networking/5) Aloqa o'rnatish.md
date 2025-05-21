## Asosiy almashinuv mexanizmlari
Kalit almashish usullari ikki tomon o'rtasida [kriptografik kalitlarni](https://www.cloudflare.com/learning/ssl/what-is-a-cryptographic-key/) xavfsiz almashish uchun ishlatiladi. Bu ko'plab kriptografik protokollarning muhim qismidir, chunki aloqani himoya qilish uchun ishlatiladigan shifrlashning xavfsizligi kalitlarning maxfiyligiga bog'liq. Ko'pgina asosiy almashinuv usullari mavjud, ularning har biri o'ziga xos xususiyatlarga va kuchli tomonlarga ega. Ba'zi kalit almashinuv usullari boshqalarga qaraganda xavfsizroqdir va tegishli usul vaziyatning o'ziga xos holatlari va talablariga bog'liq.

Bu usullar, odatda, ikki tomon o'rtasidagi aloqani shifrlaydigan xavfsiz bo'lmagan aloqa kanali orqali "umumiy maxfiy kalit" bo'yicha kelishib olishga imkon berish orqali ishlaydi. Bu, odatda, matematik funktsiyaning xususiyatlariga asoslangan hisoblash yoki kalitning bir qator oddiy manipulyatsiyasi kabi matematik operatsiyalarning ba'zi shakllari yordamida amalga oshiriladi.

#### Diffie-Hellman
Kalit almashinuvining keng tarqalgan usullaridan biri bu [Diffie-Hellman kalit almashinuvi](https://www.comparitech.com/blog/information-security/diffie-hellman-key-exchange/), bu ikki tarafga hech qanday oldindan muloqotsiz yoki umumiy shaxsiy ma'lumotlarsiz umumiy maxfiy kalit haqida kelishib olish imkonini beradi. U ikki tomon o'rtasidagi xabarlarni shifrlash va shifrini ochish uchun ishlatilishi mumkin bo'lgan umumiy maxfiy kalitni yaratish kontseptsiyasiga asoslanadi. U tez-tez xavfsiz aloqa kanallarini o'rnatish uchun asos sifatida ishlatiladi, masalan, veb-trafikni himoya qilish uchun ishlatiladigan [Transport Layer Security](https://www.cloudflare.com/learning/ssl/transport-layer-security-tls/) (`TLS`) protokoli.

"Diffie-Hellman" kalit almashinuvining asosiy cheklovlaridan biri shundaki, u "MITM hujumlari" ga nisbatan zaifdir. MITM hujumida biz ikki tomon o'rtasidagi aloqani to'xtatamiz va o'zimizni tomonlardan biri sifatida ko'rsatamiz, boshqa maxfiy kalitni yaratamiz va ikkala tomonni undan foydalanishga aldab qo'yamiz. Bu tajovuzkorga tomonlar o'rtasida yuborilgan xabarlarni o'qish va o'zgartirish imkonini beradi.

Yana bir cheklov shundaki, u umumiy maxfiy kalitni yaratish uchun nisbatan katta miqdordagi “CPU quvvati”ni talab qiladi. Bu uni kam quvvatli qurilmalarda yoki kalit tezda yaratilishi kerak bo'lgan holatlarda foydalanish uchun amaliy bo'lmasligi mumkin.

#### RSA
Yana bir kalit almashish usuli [Rivest–Shamir–Adleman](https://www.venafi.com/blog/how-diffie-hellman-key-exchange-different-rsa) (`RSA`) algoritmi boʻlib, umumiy maxfiy kalitni yaratish uchun katta tub sonlar xossalaridan foydalanadi. Bu usul katta tub sonlarni bir-biriga ko'paytirish nisbatan oson, lekin hosil bo'lgan sonni tub omillarga ko'paytirish qiyinligiga asoslanadi. Bu ikkitadan tashqari, biz ko'rib chiqishimiz kerak bo'lgan yana bir nechta narsalar mavjud. Shuningdek, u xavfsiz aloqa va ma'lumotlarni himoya qilishni talab qiluvchi ko'plab boshqa ilovalar va protokollarda keng qo'llaniladi, jumladan, lekin ular bilan cheklanmagan:
- Maxfiylik va autentifikatsiyani ta'minlash uchun xabarlarni shifrlash va imzolash
- [Secure Socket Layer](https://www.cloudflare.com/learning/ssl/what-is-ssl/) (`SSL`) va `TLS` protokollari kabi tarmoqlar orqali tranzitda ma`lumotlarni himoya qilish
- elektron hujjatlar va boshqa raqamli ma'lumotlarning haqiqiyligi va yaxlitligini ta'minlash uchun foydalaniladigan raqamli imzolarni yaratish va tekshirish;
- Kerberos tarmoq autentifikatsiya tizimi tomonidan ishlatiladigan [Kerberosda dastlabki autentifikatsiya qilish uchun umumiy kalit kriptografiyasi](https://www.ietf.org/rfc/rfc4556.txt) (`PKINIT`) protokoli kabi foydalanuvchi va qurilmalarni autentifikatsiya qilish
- Shaxsiy ma'lumotlar va maxfiy hujjatlarni shifrlash kabi maxfiy ma'lumotlarni himoya qilish

#### ECDH
[Diffie-Hellman elliptik egri chizig'i](https://medium.com/swlh/understanding-ec-diffie-hellman-9c07be338d4a) (`ECDH`) umumiy maxfiy kalitni yaratish uchun elliptik egri kriptografiyadan foydalanadigan Diffie-Hellman kalit almashinuvining variantidir. Asl Diffie-Hellman algoritmidan ko'ra samaraliroq va xavfsizroq bo'lish afzalligi, jumladan, lekin ular bilan cheklanmagan:
- “TLS” protokolidagi kabi xavfsiz aloqa kanallarini o'rnatish
- Shaxsiy kalitlar buzilgan taqdirda ham o'tgan aloqalarni oshkor qilib bo'lmasligini ta'minlaydigan oldinga maxfiylikni ta'minlash
- VPN-larda ishlatiladigan [Internet Key Exchange](https://docs.oracle.com/cd/E19683-01/816-7264/6md9iem1g/index.html) (`IKE`) protokoli kabi foydalanuvchi va qurilmalarni autentifikatsiya qilish

#### ECDSA
[Elliptic Curve Digital Signature Algoritm](https://www.hypr.com/security-encyclopedia/elliptic-curve-digital-signature-algorithm) (`ECDSA`) kalit almashinuvida ishtirok etuvchi tomonlarni autentifikatsiya qila oladigan raqamli imzolarni yaratish uchun elliptik egri kriptografiyadan foydalanadi.

Keling, ushbu algoritmlarni umumlashtiramiz va taqqoslaymiz:

| **Algoritm**                          | **Qisqartma** | **Xavfsizlik**                                                            |                                                            |
| ------------------------------------- | ------------- | ------------------------------------------------------------------------- | ---------------------------------------------------------- |
| `Diffie-Hellman`                      | `DH`          | Nisbatan xavfsiz va hisoblash samaradorligi                               |                                                            |
| `Rivest-Shamir-Adleman`               | `RSA`         | Keng qo'llaniladigan va xavfsiz deb hisoblanadi, lekin hisoblash intensiv |                                                            |
| `Eliptik egri Diffie-Hellman`         | `ECDH`        | An'anaviy Diffie-Hellman                                                  | bilan solishtirganda yaxshilangan xavfsizlikni ta'minlaydi |
| `Eliptik egri raqamli imzo algoritmi` | `ECDSA`       | Raqamli imzo yaratish uchun xavfsizlik va samaradorlikni oshiradi         |                                                            |
### Internet kalitlari almashinuvi
[Internet Key Exchange](https://www.hypr.com/security-encyclopedia/internet-key-exchange) (`IKE`) VPN-larda ishlatiladiganlar kabi xavfsiz aloqa seanslarini oʻrnatish va saqlash uchun foydalaniladigan protokoldir. U kalitlarni xavfsiz almashish va xavfsizlik parametrlarini muhokama qilish uchun “Diffie-Hellman” kalit almashinuvi algoritmi va “boshqa kriptografik usullar” kombinatsiyasidan foydalanadi. Bundan tashqari, u ko'plab VPN yechimlarining asosiy komponenti hisoblanadi, chunki u VPN mijozi va server o'rtasida kalitlar va boshqa xavfsizlik ma'lumotlarini xavfsiz almashish imkonini beradi. Bu VPN-ga ma'lumotlar xavfsiz uzatilishi mumkin bo'lgan shifrlangan tunnel o'rnatish imkonini beradi.

IKE dan boshqa maqsadlarda, masalan, foydalanuvchilar va qurilmalarni autentifikatsiya qilishda ham foydalanish mumkin. U odatda kalit almashinuvi va raqamli imzolar uchun RSA algoritmi va maʼlumotlarni shifrlash uchun [Advanced Encryption Standard](https://www.geeksforgeeks.org/advanced-encryption-standard-aes/) (`AES`) kabi boshqa protokollar va algoritmlar bilan birgalikda ishlatiladi.

IKE "asosiy rejim" yoki "agressiv rejim" da ishlaydi. Ushbu rejimlar kalit almashinuv jarayonining ketma-ketligi va parametrlarini aniqlaydi va IKE sessiyasining xavfsizligi va ishlashiga ta'sir qilishi mumkin.

#### Asosiy rejim
"Asosiy rejim" "IKE" uchun standart rejim bo'lib, odatda agressiv rejimga qaraganda "xavfsizroq" hisoblanadi. Kalit almashish jarayoni asosiy rejimda “uch bosqichda” amalga oshiriladi, ularning har biri turli xil xavfsizlik parametrlari va kalitlarni almashtiradi. Bu ko'proq moslashuvchanlik va xavfsizlikni ta'minlaydi, ammo agressiv rejimga nisbatan sekinroq ishlashga olib kelishi mumkin.

#### Agressiv rejim
"Agressiv rejim" - bu "IKE" uchun muqobil rejim bo'lib, kalit almashish uchun zarur bo'lgan aylanma sayohatlar va xabar almashishlar sonini kamaytirish orqali "tezroq ishlash" imkonini beradi. Ushbu rejimda kalitlarni almashish jarayoni “ikki bosqichda” amalga oshiriladi, birinchi bosqichda barcha xavfsizlik parametrlari va kalitlar almashtiriladi. Biroq, bu tezroq ishlashni ta'minlashi mumkin, lekin asosiy rejimga nisbatan IKE sessiyasining xavfsizligini ham kamaytirishi mumkin, chunki "agressiv rejim" identifikatsiyani himoya qilmaydi.

#### Oldindan ulashilgan kalitlar
IKE-da "Oldindan umumiy kalit" ("PSK") kalit almashinuvida ishtirok etuvchi ikki tomon o'rtasida taqsimlanadigan maxfiy qiymatdir. Ushbu kalit tomonlarni autentifikatsiya qilish va keyingi muloqotni shifrlaydigan umumiy sirni o'rnatish uchun ishlatiladi. IKE-da PSK-dan foydalanish ixtiyoriydir va uni ishlatish yoki ishlatmaslik vaziyatning o'ziga xos talablari va cheklovlariga bog'liq. Biroq, agar “PSK” ishlatilsa, kalit almashish jarayoni boshlanishidan oldin u ikki tomon o'rtasida ishonchli tarzda almashtirilishi kerak. Bu alohida aloqa kanali kabi xavfsiz tarmoqdan tashqari kanal orqali yoki kalitni jismoniy almashish orqali amalga oshirilishi mumkin.

PSK dan foydalanishning asosiy afzalligi shundaki, u tomonlarga bir-birlari bilan autentifikatsiya qilish imkonini berib, qo'shimcha xavfsizlik darajasini ta'minlaydi. Biroq, PSK dan foydalanish ham ba'zi cheklovlar va kamchiliklarga ega. Masalan, kalitni xavfsiz almashish qiyin bo'lishi mumkin va agar kalit MITM hujumi orqali buzilgan bo'lsa, IKE sessiyasining xavfsizligi buzilgan bo'lishi mumkin.

---

## Autentifikatsiya protokollari
Tarmoqlarda qurilmalar va foydalanuvchilarning identifikatorini tekshirish uchun turli xil autentifikatsiya protokollari qo'llaniladi. Ushbu protokollar muhim ahamiyatga ega, chunki ular tarmoqdagi foydalanuvchilar, qurilmalar va boshqa ob'ektlarning "identifikatsiyasini tekshirish"ning xavfsiz va standartlashtirilgan usulini ta'minlaydi. Autentifikatsiya protokollarisiz tarmoqdagi ob'ektlarni xavfsiz va ishonchli aniqlash qiyin bo'lib, buzg'unchilarga ruxsatsiz kirishni osonlashtiradi va tarmoqqa potentsial xavf tug'diradi.

Autentifikatsiya protokollari, shuningdek, biz qisqacha muhokama qiladigan tarmoqdagi ob'ektlar o'rtasida "xavfsiz ma'lumot almashish" uchun vositani taqdim etadi. Bu maxfiy ma'lumotlarning maxfiyligi va yaxlitligini ta'minlash, ruxsatsiz kirish va boshqa xavfsizlik tahdidlarining oldini olish uchun muhimdir. Keling, bir nechta eng ko'p ishlatiladigan autentifikatsiya protokollarini ko'rib chiqaylik:

| **Protocol** | **Description**                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                           |
| ------------ | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `Kerberos`   | Domen muhitida chiptalardan foydalanadigan kalitlarni tarqatish markazi (KDC) asosidagi autentifikatsiya protokoli.                                                                                                                                                                                                                                                                                                                                                                                                       |
| `SRP`        | Bu parolga asoslangan autentifikatsiya protokoli bo'lib, u tinglash va o'rtadagi odam hujumlaridan himoya qilish uchun kriptografiyadan foydalanadi.                                                                                                                                                                                                                                                                                                                                                                      |
| `SSL`        | Kompyuter tarmog'i orqali xavfsiz aloqa uchun ishlatiladigan kriptografik protokol.                                                                                                                                                                                                                                                                                                                                                                                                                                       |
| `TLS`        | TLS - bu internet orqali aloqa xavfsizligini ta'minlovchi kriptografik protokol. Bu SSL ning vorisi.                                                                                                                                                                                                                                                                                                                                                                                                                      |
| `OAuth`      | Avtorizatsiya uchun ochiq standart boʻlib, foydalanuvchilarga oʻz veb-resurslariga oʻzlarining parollarini baham koʻrmasdan uchinchi shaxslarga kirish huquqini berish imkonini beradi.                                                                                                                                                                                                                                                                                                                                   |
| `OpenID`     | OpenID - bu markazlashtirilmagan autentifikatsiya protokoli bo'lib, foydalanuvchilarga bir nechta veb-saytlarga kirish uchun bitta identifikatsiyadan foydalanish imkonini beradi.                                                                                                                                                                                                                                                                                                                                        |
| `SAML`       | Security Assertion Markup Language tomonlar o'rtasida autentifikatsiya va avtorizatsiya ma'lumotlarini xavfsiz almashish uchun XML-ga asoslangan standartdir.                                                                                                                                                                                                                                                                                                                                                             |
| `2FA`        | Foydalanuvchi identifikatorini tekshirish uchun ikki xil omil kombinatsiyasidan foydalanadigan autentifikatsiya usuli.                                                                                                                                                                                                                                                                                                                                                                                                    |
| `FIDO`       | Fast IDentity Online Alliance - bu kuchli autentifikatsiya uchun ochiq standartlarni ishlab chiqish ustida ishlaydigan kompaniyalar konsorsiumi.                                                                                                                                                                                                                                                                                                                                                                          |
| `PKI`        | PKI - bu shifrlash va raqamli imzolar uchun ochiq va yopiq kalitlardan foydalanishga asoslangan ma'lumotlarni xavfsiz almashish tizimi.                                                                                                                                                                                                                                                                                                                                                                                   |
| `SSO`        | Foydalanuvchiga bir nechta ilovalarga kirish uchun bitta hisob ma'lumotlari to'plamidan foydalanish imkonini beruvchi autentifikatsiya usuli.                                                                                                                                                                                                                                                                                                                                                                             |
| `MFA`        | TIV autentifikatsiya usuli boʻlib, uning identifikatorini tekshirish uchun foydalanuvchi biladigan narsa (parol), foydalanuvchida bor narsa (telefon) yoki foydalanuvchi oʻzi (biometrik maʼlumotlar) kabi bir nechta omillardan foydalanadi.                                                                                                                                                                                                                                                                             |
| `PAP`        | Tarmoq orqali foydalanuvchi parolini aniq matnda yuboradigan oddiy autentifikatsiya protokoli.                                                                                                                                                                                                                                                                                                                                                                                                                            |
| `CHAP`       | Foydalanuvchi identifikatorini tekshirish uchun uch tomonlama qoʻl siqishdan foydalanadigan autentifikatsiya protokoli.                                                                                                                                                                                                                                                                                                                                                                                                   |
| `EAP`        | Foydalanuvchi identifikatorini tekshirish uchun turli texnologiyalardan foydalanishga imkon beruvchi bir nechta autentifikatsiya usullarini qo'llab-quvvatlash uchun asos.                                                                                                                                                                                                                                                                                                                                                |
| `SSH`        | Bu mijoz va server o'rtasidagi xavfsiz aloqa uchun tarmoq protokoli. Biz undan buyruq qatoriga masofaviy kirish va masofaviy buyruqni bajarish, shuningdek, xavfsiz fayllarni uzatish uchun foydalanishimiz mumkin. SSH tinglash va boshqa hujumlardan himoya qilish uchun shifrlashdan foydalanadi va autentifikatsiya qilish uchun ham ishlatilishi mumkin.                                                                                                                                                             |
| `HTTPS`      | Bu Internetda muloqot qilish uchun ishlatiladigan HTTP protokolining xavfsiz versiyasidir. HTTPS aloqani shifrlash va autentifikatsiyani ta'minlash uchun SSL/TLS dan foydalanadi, bu esa uchinchi tomonlar uzatilgan ma'lumotlarni tutib olmasligini va o'qiy olmasligini ta'minlaydi. U Internet orqali xavfsiz aloqa uchun, xususan, veb-sahifalarni ko'rish uchun keng qo'llaniladi.                                                                                                                                  |
| `LEAP`       | LEAP - Cisco tomonidan ishlab chiqilgan simsiz autentifikatsiya protokoli. U simsiz mijoz va server o'rtasida o'zaro autentifikatsiyani ta'minlash uchun EAP dan foydalanadi va ikkalasi o'rtasidagi aloqani shifrlash uchun RC4 shifrlash algoritmidan foydalanadi. Afsuski, LEAP lug'at hujumlari va boshqa xavfsizlik zaifliklariga qarshi himoyasiz va asosan EAP-TLS va PEAP kabi xavfsizroq protokollar bilan almashtirildi.                                                                                        |
| `PEAP`       | Boshqa tomondan, PEAP simsiz va simli tarmoqlar uchun ishlatiladigan xavfsiz tunnel protokoli. U EAP-ga asoslangan va mijoz va server o'rtasidagi aloqani shifrlash uchun TLS-dan foydalanadi. PEAP serverni autentifikatsiya qilish uchun server tomoni sertifikatidan foydalanadi va parollar, sertifikatlar yoki biometrik ma'lumotlar kabi turli usullar yordamida mijozni autentifikatsiya qilish uchun ham foydalanish mumkin. PEAP xavfsiz autentifikatsiya qilish uchun korporativ tarmoqlarda keng qo'llaniladi. |

Masalan, LEAP va PEAP simsiz mijozlar simsiz tarmoqqa kirishda autentifikatsiya qilish yoki VPN orqali tarmoqqa ulangan masofaviy xodimlarni autentifikatsiya qilish uchun ishlatilishi mumkin. Bunday hollarda, SSH yoki HTTPS dan foydalanish qiyin bo'ladi, chunki ular turli maqsadlar uchun mo'ljallangan. Xavfsizlik nuqtai nazaridan, “PEAP” odatda LEAP’ga qaraganda xavfsizroqdir, chunki u serverni autentifikatsiya qilish va “MSCHAPv2” xeshini shifrlash uchun server tomonidagi ochiq kalit sertifikatidan foydalanadi, “LEAP” esa mijoz va server o‘rtasida kelishilgan va “MSCHAPv2”ni shifrlamaydigan umumiy sirga tayanadi. PEAP, shuningdek, autentifikatsiya ma'lumotlarini shifrlash uchun AES va 3DES kabi kuchliroq shifrlash algoritmlaridan foydalanishni qo'llab-quvvatlaydi, LEAP esa zaifroq RC4 algoritmidan foydalanadi.

Biroq, ikkala protokol ham maxsus hujumlarga qarshi himoyasiz va asosan EAP-TLS kabi xavfsizroq protokollar bilan almashtirildi.

Jismoniy ulanishlar sifatida “SSL” yoki “TLS” protokollari sukut bo'yicha ishlatiladi, masalan, “SSH” yoki “HTTPS”. Ikkala protokol ham mijoz va server o'rtasida uzatiladigan autentifikatsiya ma'lumotlarini himoya qilish uchun mustahkam shifrlash algoritmlaridan foydalanadi. Bu autentifikatsiya jarayonining xavfsizligini ta'minlash uchun zarur bo'lgan autentifikatsiya ma'lumotlarini ushlash yoki buzishni oldini olishga yordam beradi. Shuningdek, ular mijozga serverni autentifikatsiya qilish uchun raqamli sertifikatlar va "PKI" dan foydalanishni qo'llab-quvvatlaydi. Bu mijozning server identifikatorini tekshirishini ta'minlaydi va MITM hujumlarining oldini olishga yordam beradi. SSH va HTTPS keng qo'llaniladigan va yaxshi qo'llab-quvvatlanadigan protokollar bo'lib, turli xil operatsion tizimlar va qurilmalar uchun ilovalar mavjud va ularni turli muhitlarda ishlatish va joylashtirishni osonlashtiradi.

---

## TCP/UDP ulanishlari
[Transmission Control Protocol](https://en.wikipedia.org/wiki/Transmission_Control_Protocol) (`TCP`) va [User Datagram Protocol](https://en.wikipedia.org/wiki/User_Datagram_Protocol) (`UDP`) maʼlumotlar va maʼlumotlar uzatishda ishlatiladigan protokollardir. Odatda, TCP ulanishlari veb-sahifalar va elektron pochta xabarlari kabi muhim ma'lumotlarni uzatadi. Bundan farqli o'laroq, UDP ulanishlari video oqimlari yoki onlayn o'yinlar kabi real vaqtda ma'lumotlarni uzatadi.

`TCP` ulanishga yoʻnaltirilgan protokol boʻlib, u bir kompyuterdan ikkinchisiga yuborilgan barcha maʼlumotlarni qabul qilishni taʼminlaydi. Bu qo'ng'iroq to'xtatilgunga qadar ikkala tomon ham aloqada bo'lgan telefon suhbatiga o'xshaydi. Agar ma'lumotlarni jo'natishda xatolik yuzaga kelsa, qabul qiluvchi xabarni qaytarib yuboradi, shuning uchun jo'natuvchi etishmayotgan ma'lumotlarni qayta yuborishi mumkin. Bu `TCP`ni ishonchli va UDPga qaraganda sekinroq qiladi, chunki uzatish va xatolarni tiklash uchun ko'proq vaqt talab etiladi.

Boshqa tomondan, "UDP" ulanishsiz protokoldir. Tezlik ishonchlilikdan muhimroq bo'lsa, masalan, video oqimlari yoki onlayn o'yinlar uchun ishlatiladi. `UDP` bilan qabul qilingan ma`lumotlarning to`liq va xatosiz ekanligi tasdiqlanmaydi. Agar ma'lumotlarni yuborishda xatolik yuzaga kelsa, qabul qiluvchi ushbu etishmayotgan ma'lumotlarni olmaydi va uni qayta yuborish uchun hech qanday xabar yuborilmaydi. Ba'zi ma'lumotlar "UDP" bilan yo'qolishi mumkin, ammo umumiy uzatish tezroq.

### IP paketi
[Internet Protocol](https://en.wikipedia.org/wiki/Internet_Protocol) (`IP`) paketi [Ochiq tizimlar oʻzaro aloqasi](https://en.wikipedia.org/wiki/OSI_model) (`OSI`) modelining tarmoq qatlami tomonidan bir kompyuterdan boshqasiga maʼlumotlarni uzatish uchun foydalaniladigan maʼlumotlar maydonidir. U sarlavha va foydali yuk, haqiqiy yuk ma'lumotlaridan iborat.

IP-paketni konvertda yuborilgan xat deb ham tasavvur qilishimiz mumkin. Konvertda sarlavha mavjud bo'lib, unda jo'natuvchi va qabul qiluvchi to'g'risidagi ma'lumotlar, shuningdek, xatni yo'naltirish bo'yicha ko'rsatmalar, ya'ni xat qaysi pochta bo'limlari orqali yuborilishi kerak. Xatning o'zi foydali yuk, haqiqiy yuk ma'lumotlari.

#### IP sarlavhasi
IP-paketning sarlavhasi muhim ma'lumotlarga ega bo'lgan bir nechta maydonlarni o'z ichiga oladi.

| **Field**                | **Description**                                                                        |
| ------------------------ | -------------------------------------------------------------------------------------- |
| `Version`                | IP protokolining qaysi versiyasi ishlatilayotganligini ko'rsatadi                      |
| `Internet Header Length` | Sarlavha hajmini 32 bitli so'zlarda ko'rsatadi                                         |
| `Class of Service`       | Ma'lumotlarni uzatish qanchalik muhimligini anglatadi                                  |
| `Total length`           | Paketning umumiy uzunligini baytlarda belgilaydi                                       |
| `Identification (ID)`    | Kichikroq qismlarga bo'linganda paketning bo'laklarini aniqlash uchun ishlatiladi      |
| `Flags`                  | Parchalanishni ko'rsatish uchun ishlatiladi                                            |
| `Fragment Offset`        | Joriy fragment paketning qaerga joylashtirilganligini ko'rsatadi                       |
| `Time to Live`           | Paket tarmoqda qancha vaqt qolishi mumkinligini belgilaydi                             |
| `Protocol`               | TCP yoki UDP kabi ma'lumotlarni uzatish uchun qaysi protokol ishlatilishini belgilaydi |
| `Checksum`               | Sarlavhadagi xatolarni aniqlash uchun ishlatiladi                                      |
| `Source/Destination`     | Paket qayerdan yuborilganini va qayerga yuborilganligini ko'rsating                    |
| `Options`                | Marshrutlash uchun ixtiyoriy ma'lumotlarni o'z ichiga oladi                            |
| `Padding`                | Paketni to'liq so'z uzunligiga to'ldiradi                                              |

Turli tarmoqlarda bir nechta IP manzillari bo'lgan kompyuterni ko'rishimiz mumkin. Bu erda biz "IP ID" maydoniga e'tibor qaratishimiz kerak. U kichikroq qismlarga bo'linganda IP-paketning bo'laklarini aniqlash uchun ishlatiladi. Bu "16 bitli" maydon bo'lib, noyob raqam "0-65535" oralig'ida.

Agar kompyuterda bir nechta IP manzillar bo'lsa, "IP ID" maydoni kompyuterdan yuborilgan har bir paket uchun farq qiladi, lekin juda o'xshash bo'ladi. TCPdump-da tarmoq trafigi quyidagicha ko'rinishi mumkin:

#### Tarmoqni hidlash (O'zbek tili, Boy til)
```bash
IP 10.129.1.100.5060 > 10.129.1.1.5060: SIP, length: 1329, id 1337
IP 10.129.1.100.5060 > 10.129.1.1.5060: SIP, length: 1329, id 1338
IP 10.129.1.100.5060 > 10.129.1.1.5060: SIP, length: 1329, id 1339
IP 10.129.2.200.5060 > 10.129.1.1.5060: SIP, length: 1329, id 1340
IP 10.129.2.200.5060 > 10.129.1.1.5060: SIP, length: 1329, id 1341
IP 10.129.2.200.5060 > 10.129.1.1.5060: SIP, length: 1329, id 1342
```

Chiqishdan ko'rishimiz mumkinki, ikkita turli IP-manzillar 10.129.1.1 IP-manziliga paketlarni yubormoqda. Biroq, "IP ID" dan biz paketlar uzluksiz ekanligini ko'rishimiz mumkin. Bu ikkita IP-manzil tarmoqdagi bir xil xostga tegishli ekanligini aniq ko'rsatadi.

#### IP yozuvi-marshrut maydoni
IP sarlavhasidagi "Yozuv-marshrut maydoni" shuningdek, belgilangan qurilmaga marshrutni yozib oladi. Belgilangan qurilma "ICMP Echo Reply" paketini qaytarib yuborganda, paket orqali o'tadigan barcha qurilmalarning IP manzillari IP sarlavhasining "Yozuv-marshrut maydoni"da keltirilgan. Bu quyidagi buyruqdan foydalanganda sodir bo'ladi, masalan:
```bash
VOIDstrike@athena[/home/VOIDstrike]$ ping -c 1 -R 10.129.143.158

PING 10.129.143.158 (10.129.143.158) 56(124) bytes of data.
64 bytes from 10.129.143.158: icmp_seq=1 ttl=63 time=11.7 ms
RR: 10.10.14.38
        10.129.0.1
        10.129.143.158
        10.129.143.158
        10.10.14.1
        10.10.14.38


--- 10.129.143.158 ping statistics ---
1 packets transmitted, 1 received, 0% packet loss, time 0ms
rtt min/avg/max/mdev = 11.688/11.688/11.688/0.000 ms
```

Chiqish "ping" so'rovi yuborilganligini va maqsad qurilmadan javob olinganligini bildiradi va "ICMP Echo Request" paketining IP sarlavhasida "Yozish-marshrut" maydonini ham ko'rsatadi. Yo‘nalishni yozib olish maydonida maqsad qurilmaga boradigan yo‘lda “ICMP Echo Request” paketi orqali o‘tgan barcha qurilmalarning IP manzillari mavjud. Bunday holda, "Yozuv-marshrut" maydonida IP-manzillar mavjud:

| 10.10.14.38    | 10.129.0.1 | 10.129.143.158 |
| -------------- | ---------- | -------------- |
| 10.129.143.158 | 10.10.14.1 | 10.10.14.38    |

“Traceroute” vositasidan marshrutni belgilangan manzilga aniqroq kuzatish uchun ham foydalanish mumkin, bu esa marshrut qachon toʻliq kuzatilganligini aniqlash uchun TCP taym-out usulidan foydalanadi.

1. Biz IP sarlavhasida TTL 1 bo'lgan maqsadli qurilmaga TCP SYN paketini yuboramiz.
    TTL 1 dan katta bo'lgan TCP SYN paketi marshrutizatorga yetganda, TTL qiymati 1 ga kamayadi va paket keyingi qurilmaga yo'naltiriladi. Agar TTL 1 bo'lgan TCP SYN paketi marshrutizatorga etib borsa, paket o'chirib tashlanadi va yo'riqnoma bizga ICMP Time-Oshib ketgan paketini yuboradi.

2. Biz ICMP Time-Oshib ketgan paketini olamiz va paketni yuborgan routerning IP-manzilini qayd etamiz.

3. Shundan so'ng biz TTLni 1 ga oshirib, boshqa TCP SYN paketini belgilangan joyga yuboramiz.

Jarayon TCP SYN paketi maqsadli xostga yetib borguncha va maqsaddan “TCP SYN/ACK” yoki “TCP RST” javobini olguncha takrorlanadi. Belgilangan qurilmadan javob olganimizdan so'ng, biz manzilga marshrutni kuzatganimizni va traceroute jarayonini tugatganimizni bilamiz.

#### IP yuki
Foydali yuk ("IP ma'lumotlari" deb ham ataladi) paketning haqiqiy yukidir. U TCP yoki UDP kabi turli protokollardan olingan ma'lumotlarni o'z ichiga oladi.

### TCP
"Segmentlar" deb ham ataladigan TCP paketlari sarlavhalar va foydali yuklar deb ataladigan bir nechta bo'limlarga bo'lingan. TCP segmentlari yuborilgan IP-paketga o'ralgan.

Sarlavha muhim ma'lumotlarni o'z ichiga olgan bir nechta maydonlarni o'z ichiga oladi. Manba porti paket yuborilgan kompyuterni ko'rsatadi. Belgilangan port paket qaysi kompyuterga yuborilganligini ko'rsatadi. Tartib raqami ma'lumotlarning yuborilgan tartibini ko'rsatadi. Tasdiqlash raqami barcha ma'lumotlar muvaffaqiyatli qabul qilinganligini tasdiqlash uchun ishlatiladi. Tekshirish bayroqlari paket xabarning oxirini belgilash yoki yo'qligini, ma'lumotlar olinganligini tasdiqlaydimi yoki ma'lumotlarni takrorlash so'rovini o'z ichiga oladimi yoki yo'qligini ko'rsatadi. Oyna o'lchami qabul qiluvchi qancha ma'lumot olishi mumkinligini ko'rsatadi. Tekshirish summasi sarlavha va foydali yukdagi xatolarni aniqlash uchun ishlatiladi. Shoshilinch ko'rsatkich qabul qiluvchiga muhim ma'lumotlar foydali yukda ekanligi haqida ogohlantiradi.

Foydali yuk paketning haqiqiy yukidir va ikki kishi o'rtasidagi suhbat mazmuni kabi uzatilayotgan ma'lumotlarni o'z ichiga oladi.

### UDP
UDP ikkita xost o'rtasida "ma'lumotlar" (kichik ma'lumotlar paketlari) ni uzatadi. Bu ulanishsiz protokol, ya'ni ma'lumotlarni yuborishdan oldin jo'natuvchi va qabul qiluvchi o'rtasida aloqa o'rnatish shart emas. Buning o'rniga, ma'lumotlar oldindan ulanishsiz to'g'ridan-to'g'ri maqsadli xostga yuboriladi.

UDP bilan “traceroute” ishlatilsa, UDP datagram paketi maqsadli qurilmaga yetib borganda, biz “Maqsadga erishib bo‘lmaydi” va “Portga etib bo‘lmaydi” xabarini olamiz. Odatda, UDP paketlari Unix xostlarida “traceroute” yordamida yuboriladi.

### Blind Spoofing
“Koʻr-koʻrona firibgarlik” – maʼlumotlarni manipulyatsiya qilish hujumi usuli boʻlib, unda tajovuzkor maqsadli qurilmalar tomonidan yuborilgan haqiqiy javoblarni koʻrmasdan tarmoqqa notoʻgʻri maʼlumot yuboradi. Bu noto'g'ri manba va maqsad manzillarini ko'rsatish uchun IP sarlavha maydonini manipulyatsiya qilishni o'z ichiga oladi. Masalan, biz TCP paketini maqsadli xostga noto'g'ri manba va maqsad port raqamlari va noto'g'ri "Boshlang'ich tartib raqami" ("ISN") bilan yuboramiz. "ISN" - bu ulanishdagi birinchi TCP paketining tartib raqamini belgilash uchun ishlatiladigan TCP sarlavhasidagi maydon. ISN TCP paketining jo'natuvchisi tomonidan o'rnatiladi va birinchi paketning TCP sarlavhasida qabul qiluvchiga yuboriladi. Bu maqsadli xostning ulanishni olmasdan biz bilan aloqa o'rnatishiga olib kelishi mumkin.

Ushbu hujum odatda tarmoq ulanishlarining yaxlitligini buzish yoki tarmoq qurilmalari orasidagi ulanishlarni buzish uchun ishlatiladi. Bundan tashqari, tarmoq trafigini kuzatish yoki tarmoq qurilmalari tomonidan yuborilgan ma'lumotlarni ushlab turish uchun ham foydalanish mumkin.

---

### Kriptografiya
Shifrlash Internetda to'lov ma'lumotlari, elektron pochta xabarlari yoki shaxsiy ma'lumotlar kabi ma'lumotlarni maxfiy va manipulyatsiyadan himoyalangan holda uzatish uchun ishlatiladi. Ma'lumotlar matematik operatsiyalarga asoslangan turli kriptografik algoritmlar yordamida shifrlanadi. Shifrlash yordamida ma'lumotlar ruxsatsiz shaxslar o'qiy olmaydigan shaklga aylantirilishi mumkin. Shifrlash uchun “simmetrik” yoki “assimetrik” shifrlash jarayonlaridagi raqamli kalitlardan foydalaniladi. Amaldagi shifrlash usullariga qarab shifrlangan matnlarni yoki kalitlarni buzish osonroq. Keng kalit uzunliklariga ega bo'lgan zamonaviy kriptografik usullardan foydalanilsa, ular juda xavfsiz ishlaydi va hozircha murosa qilish deyarli mumkin emas. Asosan, biz "simmetrik" va "assimetrik" shifrlash usullarini farqlashimiz mumkin. Asimmetrik usullar faqat bir necha o'n yillar davomida ma'lum. Shunga qaramay, ular raqamli aloqada eng ko'p qo'llaniladigan usullardir.

#### Simmetrik shifrlash
Yashirin kalit shifrlash deb ham ataladigan simmetrik shifrlash ma'lumotlarni shifrlash va shifrini ochish uchun bir xil kalitdan foydalanadigan usuldir. Bu shuni anglatadiki, ma'lumotlarni to'g'ri hal qilish uchun jo'natuvchi va qabul qiluvchi bir xil kalitga ega bo'lishi kerak.

Agar maxfiy kalit baham ko'rilsa yoki yo'qolsa, ma'lumotlar xavfsizligi endi kafolatlanmaydi. Nosimmetrik shifrlash usullari uchun muhim harakatlar kalitlarni taqsimlash, saqlash va almashishni anglatadi. [Kengaytirilgan shifrlash standarti](https://en.wikipedia.org/wiki/Advanced_Encryption_Standard) (`AES`) va [Ma'lumotlarni shifrlash standarti](https://en.wikipedia.org/wiki/Data_Encryption_Standard) (`DES`) simmetrik shifrlashning misollaridir. Ushbu turdagi shifrlash ko'pincha qattiq diskdagi fayllar yoki tarmoq orqali yuborilgan ma'lumotlar kabi katta hajmdagi ma'lumotlarni shifrlash uchun ishlatiladi. “AES” bugungi kunda eng xavfsiz shifrlash algoritmi hisoblanadi.

#### Asimmetrik shifrlash
“Ochiq kalitli shifrlash” deb ham ataladigan assimetrik shifrlash ikki xil kalitdan foydalanadigan shifrlash usulidir:
- "ommaviy kalit"
- "maxfiy kalit"

Ochiq kalit ma'lumotlarni shifrlash uchun, shaxsiy kalit esa ma'lumotlarni shifrlash uchun ishlatiladi. Bu shuni anglatadiki, har kim kimdir uchun ma'lumotlarni shifrlash uchun ochiq kalitdan foydalanishi mumkin, lekin faqat tegishli shaxsiy kalitga ega bo'lgan qabul qiluvchi ma'lumotlarni shifrlashi mumkin. Asimmetrik shifrlash usullariga misollar: [Rivest–Shamir–Adleman](https://en.wikipedia.org/wiki/RSA_\(cryptosystem\)) (`RSA`), [Pretty Good Privacy](https://en.wikipedia.org/wiki/Pretty_Good_Good_Privacy) va [Kriptografiya](https://en.wikipedia.org/wiki/Elliptic-curve_cryptography) (`ECC`). Asimmetrik shifrlash turli xil ilovalarda qo'llaniladi, ulardan ba'zilari:

| E-Signatures | SSL/TLS | VPNs  |
| ------------ | ------- | ----- |
| SSH          | PKI     | Cloud |

### Ochiq kalit bilan shifrlash
Asimmetrik shifrlashning afzalliklaridan biri uning “xavfsizligi”dir. Xavfsizlik juda qiyin echilishi mumkin bo'lgan matematik muammolarga asoslanganligi sababli, oddiy hujumlar uni yorib bo'lmaydi. Bundan tashqari, kalitlarni almashtirish masalasi chetlab o'tiladi. Bu nosimmetrik shifrlash usullari bilan bog'liq muhim muammo. Biroq, ochiq kalit hamma uchun ochiq bo'lishi mumkinligi sababli, kalitlarni yashirincha almashishning hojati yo'q. Bundan tashqari, assimetrik usullar raqamli imzolar bilan autentifikatsiya qilish imkoniyatini ochadi.

### Ma'lumotlarni shifrlash standarti
DES simmetrik kalitli blokli shifrdir va uning shifrlanishi bit ketma-ketligiga qo'llaniladigan bir martalik pad, almashtirish va almashtirish shifrlarining kombinatsiyasi sifatida ishlaydi. U maʼlumotlarni “shifrlash va parolini ochish”da “bir xil kalitdan” foydalanadi.

Kalit "64 bit" dan iborat bo'lib, nazorat summasi sifatida "8 bit" ishlatiladi. Shuning uchun DES ning haqiqiy kalit uzunligi atigi “56 bit” ni tashkil qiladi. Va shuning uchun DESga murojaat qilganda har doim 56 bitli kalit uzunligi haqida gapiriladi. Chastotani tahlil qilish xavfining oldini olish uchun bitta harf emas, balki har bir 64 bitli ochiq matn bloki 64 bitli shifrlangan matn blokiga shifrlangan.

DES kengaytmasi [Triple DES / 3DES] (https://en.wikipedia.org/wiki/Triple_DES) deb nomlanadi, bu ma'lumotlarni xavfsizroq shifrlaydi. Buning protsedurasi odatda uchta kalitdan iborat bo'lib, birinchi kalit ma'lumotlarni shifrlash uchun, ikkinchisi ma'lumotlarni shifrlash uchun, uchinchisi esa ma'lumotlarni qayta shifrlash uchun ishlatiladi.

`3DES` asl DES-ga qaraganda xavfsizroq hisoblangan, chunki u shifrlashning uch bosqichidan foydalangan holda ko'proq xavfsizlikni ta'minlaydi, ammo 56-bitli kalitdan foydalanish hali ham uni cheklaydi. DESning vorisi bo'lgan `AES` uzunroq kalit uzunligidan foydalangan holda yuqori xavfsizlikni ta'minlaydi va hozirda eng keng tarqalgan simmetrik shifrlash texnologiyasi hisoblanadi.

### Kengaytirilgan shifrlash standarti
DES bilan solishtirganda, AES maʼlumotlarni shifrlash va shifrini ochish uchun 128-bitli (`AES-128`), 192-bitli (`AES-192`) yoki 256-bitli (`AES-256`) kalitlardan foydalanadi. Bundan tashqari, AES DESga qaraganda tezroq ishlaydi, chunki u yanada samarali algoritm tuzilishiga ega. Buning sababi shundaki, u bir vaqtning o'zida bir nechta ma'lumotlar bloklariga qo'llanilishi mumkin, bu esa uni tezroq qiladi. Bu shuni anglatadiki, AES shifrlash va shifrlash DESga qaraganda tezroq amalga oshirilishi mumkin, bu ayniqsa katta hajmdagi ma'lumotlarni shifrlash kerak bo'lganda muhimdir.

Masalan, biz AES-ni turli xil ilovalar va protokollarda topishimiz mumkin, ammo ular quyidagilar bilan cheklanmaydi:

| WLAN IEEE 802.11i | IPsec | SSH     |
| ----------------- | ----- | ------- |
| VoIP              | PGP   | OpenSSL |

### Shifrlash rejimlari
Shifrlash rejimi blokli shifrlash algoritmi ochiq matnli xabarni qanday shifrlashini bildiradi. Blok shifrlash algoritmi ma'lumotlarni shifrlaydi, ularning har biri qattiq o'lchamdagi ma'lumotlar bloklaridan (odatda 64 yoki 128 bit) foydalanadi. Shifrlash rejimi ushbu bloklar qanday ishlov berilishini va istalgan uzunlikdagi xabarni shifrlash uchun birlashtirilishini belgilaydi. Bir nechta umumiy shifrlash usullari mavjud, jumladan:

| **Cipher Mode**                                                                                                 | **Description**                                                                                                                                                                                                                                                                                       |
| --------------------------------------------------------------------------------------------------------------- | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| [Electronic Code Book](https://en.wikipedia.org/wiki/Block_cipher_mode_of_operation) (`ECB`)                    | ECB rejimi odatda ma'lum turdagi hujumlarga moyilligi tufayli foydalanish uchun tavsiya etilmaydi. Bundan tashqari, u ma'lumotlar naqshlarini samarali yashirmaydi. Natijada, statistik tahlil aniq matnli xabarlar elementlarini, masalan, veb-ilovalarda ochib berishi mumkin.                      |
| [Cipher Block Chaining](https://en.wikipedia.org/wiki/Block_cipher_mode_of_operation#CBC) (`CBC`)               | CBC rejimi odatda disk shifrlash va elektron pochta aloqasi kabi xabarlarni shifrlash uchun ishlatiladi. Bu AES uchun standart rejim bo'lib, TrueCrypt, VeraCrypt, TLS va SSL kabi dasturlarda ham qo'llaniladi.                                                                                      |
| [Cipher Feedback](https://en.wikipedia.org/wiki/Block_cipher_mode_of_operation#Cipher_feedback_\(CFB\)) (`CFB`) | CFB rejimi ma'lumotlar oqimini real vaqt rejimida shifrlash uchun juda mos keladi, masalan, tarmoq aloqasi shifrlash yoki Ochiq kalitli kriptografiya standartlari (PKCS) va Microsoft-ning BitLocker kabi tranzitdagi fayllarni shifrlash/parchalash.                                                |
| [Output Feedback](https://en.wikipedia.org/wiki/Block_cipher_mode_of_operation#OFB) (`OFB`)                     | OFB rejimi ma'lumotlar oqimini shifrlash uchun ham ishlatiladi, masalan, real vaqtda aloqani shifrlash uchun. Biroq, kalit oqimi qanday yaratilganligi sababli ushbu rejim ma'lumotlar oqimi uchun yaxshiroq deb hisoblanadi. Biz ushbu rejimni PKCS da, balki SSH protokolida ham topishimiz mumkin. |
| [Counter](https://en.wikipedia.org/wiki/Block_cipher_mode_of_operation#CTR) (`CTR`)                             | CTR rejimi AES foydalanadigan real vaqtda ma'lumotlar oqimlarini shifrlaydi, masalan, tarmoq aloqasi, diskni shifrlash va ma'lumotlar qayta ishlanadigan boshqa real vaqt stsenariylari. Bunga IPsec yoki Microsoft-ning BitLocker misol bo'lishi mumkin.                                             |
| [Galois/Counter](https://en.wikipedia.org/wiki/Galois/Counter_Mode) (`GCM`)                                     | GCM simsiz aloqa, VPN va boshqa xavfsiz aloqa protokollari kabi maxfiylik va yaxlitlikni birgalikda himoya qilish zarur bo'lgan hollarda qo'llaniladi.                                                                                                                                                |

Har bir rejim o'ziga xos xususiyatlarga ega va muayyan foydalanish holatlari uchun ko'proq mos keladi. Shifrlash rejimini tanlash dastur talablariga va erishilishi kerak bo'lgan xavfsizlik maqsadlariga bog'liq.