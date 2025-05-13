Ikkita tarmoq modeli “ISO/OSI modeli” va “TCP/IP modeli” ma’lumotlarni bir xostdan ikkinchisiga uzatilgan bitlarni biz uchun o'qilishi mumkin bo'lgan tarkibda ifodalovchi "qatlamlar" ning soddalashtirilgan tasviri.

![Model_Layers](https://academy.hackthebox.com/storage/modules/34/redesigned/net_models4.png)

---

## ISO/OSI Model

Ko'pincha "ISO/OSI" deb ataladigan "OSI" modeli tizimlar orasidagi aloqani tavsiflash va aniqlash uchun qo'llanilgan modelidir. "OSI" atamasi "Xalqaro elektr aloqa ittifoqi" ("ITU") va "Xalqaro standartlashtirish tashkiloti" ("ISO") tomonidan nashr etilgan "Ochiq tizimlar o'zaro bog'liqligi" modelini anglatadi. Shuning uchun "OSI" modeli ko'pincha "ISO/OSI" modeli deb ataladi.

“ISO/OSI” standartini yaratishdan maqsad turli qurilmalar va texnologiyalar orqali turli texnik tizimlarning aloqasini va moslikni taʼminlovchi modelni yaratish edi. “OSI” modeli ushbu maqsadga erishish uchun bir-biriga asoslangan 7 turli qatlamlardan foydalanadi.

| **Layer**                | **Function**                                                                                                                                                                                                                        |
| ------------------------ | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `7.Ilova`                | Boshqa narsalar qatorida, bu qatlam ma'lumotlarni kiritish va chiqarishni boshqaradi va dastur funktsiyalarini ta'minlaydi.                                                                                                         |
| `6.Taqdimot`             | Taqdimot qatlamining vazifasi tizimga bog'liq bo'lgan ma'lumotlar taqdimotini dasturdan mustaqil shaklga o'tkazishdir.                                                                                                              |
| `5.Sessiya`              | Sessiya qatlami ikki tizim o'rtasidagi mantiqiy aloqani boshqaradi va, tarmoqda uzilishi yoki boshqa muammolarni oldini oladi.                                                                                                      |
| `4.Transport`            | 4-qatlam uzatilgan ma'lumotlarni oxirigacha nazorat qilish uchun ishlatiladi. Transport qatlami tirbandlik holatlarini va segment ma'lumotlar oqimini aniqlashi va oldini olishi mumkin.                                            |
| `3.Tarmoq`               | Tarmoq sathida ulanishlar sxemali kommutatsiyalangan tarmoqlarda o'rnatiladi va ma'lumotlar paketlari paketli kommutatsiyalangan tarmoqlarda uzatiladi. Ma'lumotlar jo'natuvchidan qabul qiluvchiga butun tarmoq bo'ylab uzatiladi. |
| `2.Ma'lumotlar havolasi` | 2-qatlamning asosiy vazifasi tegishli muhitda ishonchli va xatosiz uzatishni ta'minlashdir. Shu maqsadda 1-qatlamdagi bit oqimlari bloklarga bo'linadi.                                                                             |
| `1.Physical`             | Amaldagi uzatish usullari, masalan, elektr signallari, optik signallar yoki elektromagnit to'lqinlar. 1-qatlam orqali uzatish simli yoki simsiz uzatish liniyalarida amalga oshiriladi                                              |

"2-4" qatlamlari "transportga yo'naltirilgan" va "5-7" qatlamlari "ilovaga yo'naltirilgan" qatlamlardir. Har bir qatlamda aniq belgilangan vazifalar bajariladi va qo'shni qatlamlarga aniq tasvirlanadi. Har bir qatlam to'g'ridan-to'g'ri uning ustidagi qatlamga foydalanish uchun xizmatlarni taklif qiladi. Ushbu xizmatlarni mavjud qilish uchun qatlam o'zining ostidagi qatlam xizmatlaridan foydalanadi va o'z qatlamining vazifalarini bajaradi.

Agar ikkita tizim o'zaro aloqa qilsa, "OSI" modelining barcha 7 qatlami kamida "ikki marta" ishlaydi, chunki jo'natuvchi ham, qabul qiluvchi ham qatlam modelini hisobga olishi kerak. Ilova paketni boshqa tizimga yuborganda, tizim yuqorida ko'rsatilgan qatlamlarni "7"chi qatlamdan "1"chi qatlamgacha ishlaydi va qabul qiluvchi tizim qabul qilingan paketni "1"chi qatlamdan "7"chi qatlamgacha ochadi. Shuning uchun, aloqa xavfsizligi, ishonchliligi va barqarror ishlashini ta'minlash uchun har bir qatlamlarda juda ko'p turli xil vazifalar bajarilishi kerak.

---

## TCP/IP Model

`TCP/IP` ko'pgina tarmoq protokollari uchun umumiy atamadir. Protokollar Internetda ma'lumotlar paketlarini almashtirish va tashish uchun javobgardir. Internet butunlay “TCP/IP” protokollari oilasiga asoslangan. 

"TCP/IP" nafaqat ushbu ikkita protokolga ishora qiladi, balki butun protokollar oilasi uchun ham umumiy atama sifatida ishlatiladi. Masalan, `ICMP` (`Internet Control Message Protocol`) yoki `UDP` (`User Datagram Protocol`) protokollar oilasiga tegishli. Protokollar oilasi shaxsiy yoki umumiy tarmoqda ma'lumotlar paketlarini tashish va almashtirish uchun zarur funktsiyalarni ta'minlaydi.

"TCP/IP" modeli ham qatlamli modeli bo'lib, ko'pincha "Internet Protocol Suite" deb ataladi. "TCP/IP" atamasi "Transmission Control Protocol" ("TCP") va "Internet Protocol" ("IP") ikkita protokolni anglatadi. `IP` `tarmoq qatlami` (`qatlam 3`) ichida, `TCP` esa `OSI` qatlami modelining `transport qatlami` (`Layer 4`) ichida joylashgan.

| **Layer**     | **Function**                                                                                                                                                   |
| ------------- | -------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `4.Ilova`     | Ilova qatlami ilovalarga boshqa qatlamlar xizmatlariga kirish imkonini beradi va ilovalar ma'lumotlar almashish uchun foydalanadigan protokollarni belgilaydi. |
| `3.Transport` | Transport qatlami Ilova qatlami uchun (TCP) sessiya va (UDP) datagram xizmatlarini taqdim etish uchun javobgardir.                                             |
| `2.Internet`  | Internet qatlami xost manzillash, qadoqlash va marshrutlash funktsiyalari uchun javobgardir.                                                                   |
| `1.Bog'lam`   | Bog'lam qatlami TCP/IP paketlarini tarmoq muhitiga joylashtirish va tarmoq muhitidan mos keladigan paketlarni qabul qilish uchun javobgardir.                  |
`TCP/IP` yordamida har bir ilova istalgan tarmoq orqali ma'lumotlarni uzatishi va almashishi mumkin va qabul qiluvchining qayerda joylashganligi muhim emas. `IP` ma'lumotlar paketining belgilangan manzilga yetib borishini ta'minlaydi va `TCP` ma'lumotlar uzatilishini nazorat qiladi va ma'lumotlar oqimi va ilova o'rtasidagi aloqani ta'minlaydi. "TCP/IP" va "OSI" o'rtasidagi asosiy farq qatlamlar soni bo'lib, ularning ba'zilari birlashtirilgan.

![Comparison of OSI and TCP/IP models: OSI has 7 layers including Application, Presentation, Session, Transport, Network, Data-Link, and Physical. TCP/IP has 4 layers: Application, Transport, Internet, and Link.](https://academy.hackthebox.com/storage/modules/34/redesigned/net_models4.png)

"TCP/IP" ning eng muhim vazifalari:

| **Task**                     | **Protocol** | **Description**                                                                                                                                                                                                                                                                                                                                                               |
| ---------------------------- | ------------ | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `Mantiqiy manzillash`        | `IP`         | Turli tarmoqlarda ko'plab xostlar mavjudligi sababli, tarmoq topologiyasi va mantiqiy manzillashni tuzish zarurati tug'iladi. TCP/IP doirasida IP tarmoqlar va tugunlarning mantiqiy manzillarini oladi. Ma'lumotlar paketlari faqat ular bo'lishi kerak bo'lgan tarmoqqa etib boradi. Buni amalga oshirish usullari "tarmoq sinflari", "pastki tarmoq" va "CIDR" dan iborat. |
| `Marshrutlash`               | `IP`         | Har bir ma'lumot paketi uchun jo'natuvchidan qabul qiluvchigacha bo'lgan yo'l aniqlanadi. Shunday qilib, qabul qiluvchining manzili jo'natuvchiga aniq bo'lmasa ham paket aniq yetib boradi.                                                                                                                                                                                  |
| `Xato va boshqaruv oqimi`    | `TCP`        | Yuboruvchi va qabul qiluvchi virtual ulanish orqali bir-biri bilan aloqada bo'ladi. Shuning uchun ulanish hali ham o'rnatilganligini tekshirish uchun nazorat xabarlari doimiy ravishda yuboriladi.                                                                                                                                                                           |
| `Ilovani qo'llab-quvvatlash` | `TCP`        | TCP va UDP portlari ma'lum ilovalar va ularning aloqa bog'lamlarini ajratish uchun dasturiy ta'minot abstraktsiyasini tashkil qiladi.                                                                                                                                                                                                                                         |
| `Nom o'lchamlari`            | `DNS`        | DNS IP-manzillardagi FQDN orqali nomlarni aniqlashni ta'minlaydi, bu bizga internetda ko'rsatilgan nom bilan kerakli xostga kirishga imkon beradi.                                                                                                                                                                                                                            |

---

## ISO/OSI vs. TCP/IP

`TCP/IP` — xostlarga internetga ulanish imkonini beruvchi aloqa protokoli. Bu Internetdagi ilovalarda va ular tomonidan qo'llaniladigan "Transmission Control Protocol" ga ishora qiladi. "OSI" dan farqli o'laroq, u umumiy ko'rsatmalarga rioya qilingan holda, bajarilishi kerak bo'lgan qoidalarni yengillashtirishga imkon beradi.

O'z navbatida, "OSI" tarmoq va oxirgi foydalanuvchilar o'rtasidagi aloqa shlyuzidir. Shuningdek, u qat'iy protokoli va cheklovlari bilan mashhur.

---

## Paket o'tkazmalari

Qatlamli tizimda qatlamdagi qurilmalar `protokol ma'lumotlar birligi` (`PDU`) deb nomlangan boshqa formatda ma'lumotlarni almashadilar. Misol uchun, biz kompyuterda veb-saytni ko'rib chiqmoqchi bo'lganimizda, masofaviy server dasturi birinchi navbatda talab qilingan ma'lumotlarni amaliy qatlamga uzatadi. U qatlamma-qatlam qayta ishlanadi, har bir qatlam o'ziga yuklangan funktsiyalarni bajaradi. Keyin ma'lumotlar server yoki boshqa qurilma qabul qilmaguncha tarmoqning jismoniy qatlami orqali uzatiladi. Ma'lumotlar qatlamlar bo'ylab qayta yo'naltiriladi, har bir qatlam qabul qiluvchi dasturiy ta'minot ma'lumotlardan foydalanmaguncha o'ziga tayinlangan operatsiyalarni bajaradi.

![Comparison of OSI and TCP/IP models with PDUs: OSI has 7 layers including Application, Presentation, Session, Transport, Network, Data-Link, and Physical. TCP/IP has 4 layers: Application, Transport, Internet, and Link. PDUs are Data, Segment/Datagram, Packet, Frame, and Bit.](https://academy.hackthebox.com/storage/modules/34/redesigned/net_models_pdu2.png)

Uzatish vaqtida har bir qatlam paketni boshqaradigan va identifikatsiya qiluvchi yuqori qatlamdan “PDU”ga “sarlavha” qo‘shadi. Bu jarayon "kapsulyatsiya" deb ataladi. Sarlavha va ma'lumotlar birgalikda keyingi qatlam uchun PDU ni tashkil qiladi. Jarayon "Jismoniy qatlam" yoki "Tarmoq qatlami" ga qadar davom etadi, bu yerda ma'lumotlar qabul qiluvchiga uzatiladi. Qabul qiluvchi jarayonni o'zgartiradi va sarlavha ma'lumotlari bilan har bir qatlamdagi ma'lumotlarni ochadi. Shundan so'ng, dastur nihoyat ma'lumotlardan foydalanadi. Bu jarayon barcha ma'lumotlar yuborilmaguncha va qabul qilinmaguncha davom etadi.

![Diagram of packet transfer showing data encapsulation from sender to receiver through layers: Data, TCP, IP, MAC, and Binary Transmission, with corresponding headers and sequence.](https://academy.hackthebox.com/storage/modules/34/packet_transfer.png)

Biz uchun  ikkala model ham foydalidir. "TCP/IP" yordamida biz butun ulanish qanday o'rnatilganligini tezda tushuna olamiz va "ISO" yordamida biz uni qismlarga bo'lib, batafsil tahlil qilishimiz mumkin. Bu ko'pincha biz ma'lum tarmoq trafigini tinglashimiz va ushlab turishimiz mumkin bo'lganda sodir bo'ladi.