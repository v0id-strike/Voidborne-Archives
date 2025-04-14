# "Har bir buyruqni o‘rgan, har bir shiverni yech, va sayohatingizda hech qanday toshni o‘zgartirmang. Har bir mavzuni — katta yoki kichik — qabul qiling, kiberxavfsizlikning soyali olamlarida meros qoldirishingiz uchun."

---
### **1-bosqich: Shadow-Lab – Kiber Qo‘rg‘onini Qurish**

**Maqsad**: _Sizning raqamli jang maydoningizning asosini qo‘yish — asosiy mashinalarni joylashtirish, xavfsiz tarmoqlarni yaratish va o‘z domeningizning arxitekturasini shakllantirish._

- **Domenni kengaytirish**  
  *Dunyo qurilmasa, urush boshlanmaydi. VirtualBoxda virtual domenni qurib, har bir mashinaning rolini belgilash. OPNsense darvozalarni himoya qiladi, AthenaOS qilichni ko‘taradi, Ubuntu Server qorong‘ilikda shivirlashadi, Arch Linux ruхni yaratadi, Metasploitable va Fedora Server exile’da qoladi, taqdiri kutmoqda.*

- **Firewally boshidan**  
  *Birinchi himoyachini chaqiring — OPNsense-ni o‘rnatib, domeningizning qoralig‘iga qarshi himoyachisi sifatida sozlash. Uchta muqaddas yo‘lni belgilash: NAT tashqi dunyo uchun, LAN ishonchli markaz uchun va DMZ forsakenlar uchun.*

- **Huquqbuzarning tug‘ilishi**  
  *Qorong‘ulikdan AthenaOS uyg‘onadi — kiber soyalaridagi qilichingiz. Penetratsiya vositalarini sozlash, ekspluatatsiyalar arsenali yaratish va uni LANga joylashtirish.*

- **Sirlarga So‘nggi Qarash**  
  *Ubuntu Server jimning ijrochisi sifatida uyg‘onadi — C2 operatsiyalari va veb xosting uchun yashirin yo‘llarni yaratish. SSH bilan tuzilishini shakllantiring, qalqonlarini sozlang va uning shivirlari pardaning ortida eshitilmasligini ta’minlang.*

- **Arxitektning naqshlari**  
  *Arch Linux, haykaltrening asari, sizning ko‘rinishingizni kutmoqda. Uni mukammallikka keltiring — muhitni o‘rnating, interfeysni shakllantiring va tizimni qat’iyat bilan boshqaring.*

- **Qochqinlar**  
  *Firewallyning inoyatidan tashqarida, DMZda, qulaganlarning qoldiqlari kutmoqda. Metasploitable, buzilgan, ammo zaifliklarga to‘la, va Fedora Server, Docker olamining darvozasiga kirish — ularni chiqarib, sinovdan o‘tkazing, zabt eting, o‘rganing.*

---
### **2-bosqich: CLI-Inferno – Terminalning Ochiq Yoriqlari**

**Maqsad**: *Mashinalaringiz bilan bir bo‘ling — har bir buyruq, skript va tizim sirlarini o‘rganing.*

- **Yangi tug‘ilgan Terminal**  
  *Eng boshlanishdan: bir nechta Linux distribyutivlarini (Arch, Ubuntu, Fedora, Debian) Live USB va virtual mashinalar orqali o‘rnatish. Asoslarni o‘rganing — kataloglar orqali harakatlanish, fayllarni manipulyatsiya qilish (ls, cd, cp, mv, rm) va Linux fayl tizimi tuzilmasini tushunish.*

- **Man sahifalarining ilhomi**  
  *Qadimgi parchalarga murojaat qiling — man sahifalari, info buyruqlari va onlayn hujjatlar — har bir buyruq va tizim yordamchi dasturini o‘rganish.*

- **Faylning xronikasi**  
  *Fayl ruxsatnomalari, egalik va Unix fayl tizimining sirlarini kashf eting. Simvolik havolalar, qattiq havolalar va fayl tizimlarini chmod, chown va umask orqali qanday boshqarishni o‘rganing.*

- **Shell simfoniyasi**  
  *Bash va Zsh yordamida chiroyli shell skriptlarini yozing. O‘zgaruvchilar, sikllar, shartlar, funktsiyalarni o‘rganing va kundalik vazifalarni avtomatlashtirish orqali tizimingizning ishlashini muvofiqlashtiring.*

- **Daemonning shiviri**  
  *Orqa jarayonlar sirlarini oching: tizim jurnalini (syslog, journalctl), jarayonlarni boshqarish (ps, top, htop) va strace, ltrace, gdb yordamida nosozliklarni tekshirishni o‘rganing.*

- **Xaltalar va Bolg‘a**  
  *O‘zingizning Linux yadroingizni to‘g‘ri kompilyatsiya qiling, tizim chaqiruvlarini sozlang va oddiy yadro modullarini yozing. Mashinangizning urishini his eting.*

- **Xavfsizlikni himoya qilish**  
  *Himoya asoslarini qo‘yish: firewalllarni (iptables, nftables) sozlash, SELinux va AppArmor kabi xavfsizlik tizimlarini o‘rganish va tizimingizni raqamli qorong‘ilikdan himoya qilish.*

- **Kontainerlar va Forensika**  
  *Docker, Podman, LXC bilan kontainerizatsiya kuchidan foydalaning. Keyin, sirlar kashf etilishi kerak bo‘lsa, forensika vositalari (dd, foremost, Autopsy) yordamida jurnallarni, disk rasmlarini va tizim artefaktlarini tahlil qiling.*

---
### **3-bosqich: Tarmoq Urushlari – Raqamli Cheksizlikda Sayohat**

**Maqsad**: *Kompyuterlarni birlashtiradigan ko‘rmas iplarni tushunish va boshqarish.*

- **Efirning uyg‘onishi**  
  *Tarmoq apparatlari va protokollarining asoslari bilan boshlang. Tarmoq interfeyslari, Ethernet, Wi-Fi va ulanishni sinovdan o‘tkazish va monitoring qilish vositalarini o‘rganing.*

- **Haqiqiyatning qatlamlari**  
  *OSI modelini va TCP/IP stekini dekodlash. IP manzillari, subnetlash, DNS, DHCP va ARPning sehrini o‘rganing.*

- **Protokollar opera**  
  *Tarmoq simfoniyasining har bir notasi bilan tanishing: TCP, UDP, ICMP, HTTP/S, FTP, SMTP, SSH va boshqalar. Har bir protokol qanday muloqot qilishini va o‘zaro aloqalarini tushuning.*

- **Arxitektning loyihasi**  
  *Tarmoqlarni loyihalash va sozlash — routerni, switchlarni, VLAN-larni, NAT va port yo‘naltirishni o‘rnatish. O‘z mini Internetingizni labaratoriyada qurish va xavfsizligini ta’minlash.*

- **Tarmoqlardan shivirlash**  
  *Wireshark, tcpdump, tshark yordamida paketlarni tahlil qilish san’ati bilan tanishing. Tarmoq trafigini tahlil qiling, anomaliyalarni aniqlang va ma'lumot paketlarining tiliga qobiliyatli bo‘ling.*

- **Proksilar va pardalar**  
  *Proksilarni o‘rnatish, VPN-larni (OpenVPN, WireGuard) o‘rganish va TOR tarmog‘ining murg‘ak olamiga sayohat qilish. Raqamli izingizni yashirish uchun texnikalarni o‘rganing.*

- **Raqamli qal’alar**  
  *Firewalls (pfSense, iptables) va tarmoqni o‘rganishga yordam beradigan SIEM tizimlarini qurish. Tarmoq xavfsizligi hodisalarini tahlil qilishni o‘rganing.*

- **Ko‘rinmas o‘tkazish**  
  *SSH tunneling, proxychains, VPN pivoting va tarmoqlar orasidagi harakatlarning san’ati bilan tanishing.*

---
### **4-bosqich: Qizil Tungi – Soyalar Bilan Raqs**

**Maqsad**: *Raqibning poyabzaliga qadam qo‘ying — xavfsizlikni tushuning, simulyatsiya qiling va oxir-oqibat, hujumni o‘zlashtiring.*

- **Qanday qilishni o‘rganish**  
  *Insoniy jihatdan boshlang: phishing, vishing va pretexting kabi ijtimoiy muhandislik texnikalarini o‘rganing. Persuaziyani qurol sifatida ishlatishni va unga qarshi himoya choralarini o‘rganing.*

- **Kompyuterni to‘liq urish**  
  *Xavfsizlikni buzish: Exploitlar, Metasploit, Netcat va boshqa hujum vositalari bilan mashq qilish. Tizimlarni chiroyli tarzda buzishni, zaifliklarni to‘g‘ri tahlil qilishni o‘rganing.*

- **Ko‘rsatilgan urushlar**  
  *Fayl buzilishi, tarmoqqa zarar yetkazish, XSS, SQLi, RCE kabi hujumlarni muvaffaqiyatli amalga oshiring. Yaxshi tushuning va himoya qilishni ko‘rsating.*

- **Kiberhujumning qoidalari**  
  *Keyinchalik butun loyihalarning xavfsizligini tekshirib chiqish va javob tizimlarini qo‘llab-quvvatlash. Tarmoq va tizimlarni to‘g‘ri himoya qilishni amalga oshiring.*

---
### **5-bosqich: Zararli Dasturlar San’ati – Raqamli Sehrgarlikni Yaratish**

**Maqsad**: *Kam darajadagi koddan tortib, ko‘zdan kechirilmaydigan implantlarga qadar—soya ichida yashirinish va mustahkamlanish uchun zararli dasturlar yaratishni o‘rganing.*

- **Alkimyogar Dasturi**  
  *C dasturlash tili va C++ ga kirish bilan asos soling. Dasturiy ta’minotning apparat bilan qanday o‘zaro aloqada bo‘lishini va xotira boshqaruvining nozik tomonlarini tushunib oling.*

- **Kadimgi Dastur Kodlari**  
  *x86/x64 Assembly tiliga kirib boring. Assembly kodlarini o‘qish va yozishni o‘rganing, protsessor buyruqlarini tushuning va mashinangizning ichki ishlashini anglab yeting.*

- **Jim Kod**  
  *Birinchi shellkodni yarating. Jarayonni inyeksiya qilish, kod g‘orlarini yaratish va aniqlanishdan o‘tkazilmasdan payloadlar yaratish texnikalarini o‘rganing.*

- **Zaharning Tuzilishi**  
  *PE va ELF fayl formatlarini tahlil qiling—ijro etiladigan fayllar qanday yaratilishini tushuning va bu strukturalarni ekspluatatsiya va himoya uchun qanday manipulyatsiya qilishni o‘rganing.*

- **Mashinani Ko‘rish**  
  *IDA Pro, Ghidra va radare2 kabi teskari muhandislik vositalari bilan tanishing. Zararli dasturlar namunalarini tahlil qilish va ularning sirlarini aniqlash bo‘yicha mashq qiling.*

- **Noaniq Sehrlar**  
  *Obfuskatsiya, pakkalash va polimorfizm bilan tajriba qiling. Kodingizni antiviruslar va statik tahlil vositalaridan yashirish usullarini o‘rganing.*

- **Qochish Raqsi**  
  *Anti-debugging va sandboxdan qochish texnikalarini o‘rganing. Zararli dasturlar virtual muhitlarni qanday aniqlashini va ularni tahlil qilishdan qochishini tushuning.*

- **Doimiy Soyalar**  
  *Registrni manipulyatsiya qilish, rejalashtirilgan vazifalar, xizmatlar va hatto bootkitlardan foydalangan holda doimiylik mexanizmlarini yaratish. Raqamli mavjudligingizni bezovta qilmasdan va mustahkam holda saqlang.*

- **O‘liklarning Buyrug‘i**  
  *O‘z Command & Control (C2) infratuzilmalaringizni yarating. Zararli dastur va uning boshqaruv markazi o‘rtasidagi yashirin aloqa kanallarini yaratishni o‘rganing.*

- **So‘nggi Sehr**  
  *O‘z malakalaringizni birlashtirib, maxsus implantni yarating—soya, doimiylik va samarali kommunikatsiyani birlashtirib, raqamli sehrgarlikdagi ustunligingizni namoyish qiling.*

### **6-bosqich: Hakerlar Merosi – O‘limdan O‘zgacha O‘zgarish**

**Maqsad**: *Faqat tajribali mutaxassis bo‘lish emas, balki kiber sohada ustoz, mentor va innovator sifatida paydo bo‘lish.*

- **Katta Talon**  
  *To‘liq miqyosdagi qizil jamoa faoliyatlarini rejalashtiring va amalga oshiring. Ko‘p vektorli hujumlar strategiyalarini ishlab chiqaring, simulyatsiya qilingan raqib operatsiyalarini muvofiqlashtiring va har bir muvaffaqiyatli buzilishdan ham, har bir muvaffaqiyatsizlikdan ham o‘rganing.*

- **Ustozning Kodexi**  
  *Xavf tahlili, hodisa javob berish va ilg‘or raqamli forensika bo‘yicha tajribangizni oshiring. Murakkab zararli dasturlarni teskari muhandislikdan o‘tkazing va jamiyatga yangi bilimlar qo‘shing.*

- **Abadiy Kutubxona**  
  *Har doim zamonaviy texnologiyalarga moslashing: IoT xavfsizligi, bulutga asoslangan himoya tizimlari, konteyner xavfsizligi va AI asosida kiber urushning yangi olamlarini o‘rganing. Texnologiyalar rivojlanishi bilan bilimlaringizni doimiy ravishda yangilang.*

- **Shifrlovchining Taqdiri**  
  *Ilg‘or kriptografiyani o‘rganing, kvant hisoblashning ta’sirini o‘rganing va kiberxavfsizlikning kelajagi haqida chuqur izlanishlar olib boring. Doimo oldinga qarab yurish va texnologiyalardan oldinda bo‘lishni ta’minlang.*
