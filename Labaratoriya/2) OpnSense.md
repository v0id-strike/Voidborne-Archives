## Nima uchun OPNsense?

Raqamli urush sohasida OPNsense xavfsizlik, moslashuvchanlik va ochiq manba erkinligini muvozanatlashtiradigan kuchli qo'riqchi sifatida turadi. Bu sizga tarmoqni boshqarish, mudofaa kuchlarini mustahkamlash va trafikni aniqlik bilan boshqarish imkoniyatini beradi - bu har qanday kiberxavfsizlik amaliyotchisi uchun muhim tayanch hisoblanadi.

- ISOni yuklab olish [OPNsense.org](https://opnsense.org/)

---
## 📌 1-bosqich: OPNsense-ni sozlash

### Install OPNsense
1. OPNsense **ISO** ni mashinaga ulang va uni ishga tushiring.
2. Jonli yuklash uchun tizimga kiring: 
	- **Foydalanuvchi nomi:** `installer` 
	- **Parol:** `opnsense`
3. Klaviatura turini tanlang.
4. **ZFS (ishonchliligi uchun tavsiya etiladi)** ni tanlang.
5. **Stripe** (Single Disk) ni tanlang.
6. O'rnatish diskini tanlang va o'chirishni tasdiqlang.
7. O'rnatilgandan so'ng **ISOni olib tashlang** va qayta ishga tushiring.

---

## 📌 2-bosqich: Dastlabki konfiguratsiya

### Tarmoq interfeyslarini tayinlash
1. Kirish: **root / opnsense**
2. **1-variant: Interfeyslarni tayinlash**-ni tanlang. 
	- **WAN** → `em0` 
	- **LAN** → `em1` 
	- **DMZ** → `em2`

### LAN va DMZ IP-larni sozlang
1. **2-variant: IP interfeysini o‘rnatish**-ni tanlang. 
	- **LAN (em1):** 
		- IP: `192.168.56.2/24` 
		- Gateway yo'q 
		- DHCP-ni yoqish: **Ha** (`192.168.56.10 - 200`) 
	- **DMZ (em2):** 
		- IP: `192.168.57.1/24` 
		- Gateway yo'q 
		- DHCP-ni yoqish: **Ha** (`192.168.57.10 - 200`)
2. **12-variant: tizimni yangilash**-ni ishga tushiring.

---

## 📌 3-bosqich: xavfsizlik devori va NATni sozlash

### OPNsense Web GUI-ga kirish
1. Brauzerni oching.
2. O'ting: `http://192.168.56.2`
3. Kirish: **root / opnsense**
4. O'rnatish ustasini bajaring.
5. **Interfeyslar** ostida **OPT1** nomini **DMZ** ga o‘zgartiring.

### Internetga kirish uchun NAT-ni yoqing
1. **Firewall > NAT > Outbound**-ga o‘ting.
2. **Manual Mode**-ni tanlang.
3. **birinchi qoida** yarating: 
	- **Interfeys:** WAN 
	- **Manba manzili:** LAN Net 
	- **Qabul qiluvchi mazili:** Har qanday 
	- **Tarjima:** Interfeys manzili 
	- **Tavsif:** `"LAN Internetga kirishga ruxsat berish"`
4. **O‘zgarishlarni qo‘llash** tugmasini bosing.

### Xavfsizlik devori qoidalarini sozlash

#### 🛡️ DMZ Rules (Firewall > Rules > DMZ)
🚫 **DMZ-ga Internetga kirishni bloklash**
- Action: **Block**
- Protocol: **Any**
- Source: **DMZ Net**
- Destination: **WAN Net**
- **Apply Changes** tugmasini bosing
🚫 **DMZ ning LANga kirishini bloklash**
- Action: **Block**
- Protocol: **Any**
- Source: **DMZ Net**
- Destination: **LAN Net**
- **Apply Changes** tugmasini bosing

#### 🛡️ LAN Rules (Firewall > Rules > LAN)
✅ **LANga barcha tarmoqlarga kirishga ruxsat berish**
- Action: **Pass**
- Protocol: **Any**
- Source: **LAN Net**
- Destination: **Any**
- **Apply Changes** tugmasini bosing

---

## 📌 4-bosqich: Sinov va monitoring

### Tarmoqqa ulanishni tekshiring
✅ Ulangan qurilmalar DHCP dan IP qabul qilishini tekshiring.
✅ LAN va DMZ dan **Internetga kirishni** sinab ko'ring.
✅ Ping ** DMZ dan LAN** (bloklanishi kerak).
✅ LAN-dan **DMZ veb-serveriga kiring** (ishlashi kerak).

### Xavfsizlik devori va jurnallarni kuzatib boring
1. **Firewall > Log Files > Live View** ga o‘ting.
2. Bloklangan ulanishlarni qidiring.
3. Tarmoqli kengligidan foydalanish uchun **Interfeys Traffic Graphs** ni tekshiring.

---

## 📌 5-bosqich: Kengaytirilgan xavfsizlik xususiyatlari

### 🔐 Intrusion Detection (Suricata)
1. **Services > Intrusion Detection** ga o'ting.
2. **WAN va LANda IDS/IPS** ni yoqing.
3. **ET Open Ruleset**-ni yuklab oling.

### 🛡️ VPN Access (WireGuard)
1. **Services > WireGuard** ga o'ting.
2. **Local Endpoint** qo‘shing (OPNsense).
3. **Peers** qo‘shing (masofaviy qurilmalar).
4. **LAN interfeysiga** yo'naltiring.
5. Istalgan joydan xavfsiz ulaning.

### 🚨 Port Forwarding (Exposing Services)
1. **Firewall > NAT > Port Forward** ga o'ting.
2. Misol: **DMZ veb-serverini ochish** 
	- **Interfeys:** WAN 
	- **Mo'ljal:** WAN manzili 
	- **Port:** `8080 → 192.168.57.100:80` 
3. Tashqaridan kirishni sinab ko'ring.

---

## 📌 Phase 6: Zaxira, va yangilanishlar

### **🛠️ System Maintenance**
✅ **Mikrodasturlarni muntazam yangilash** (System > Firmware).  
✅ **Avtomatik zaxiralash** (System > Configuration > Backup).  
✅ **High Availability (HA)** (System > High Availability) ikkita OPNsense xavfsizlik devorini sinxronlashtirish uchun.