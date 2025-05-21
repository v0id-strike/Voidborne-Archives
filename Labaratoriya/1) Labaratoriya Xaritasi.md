## **Maqsad**

Ushbu laboratoriya Red Teaming, tizim boshqaruvi va Linuxni sozlashda amaliy o'rganish uchun qurilgan. U haqiqiy hujum/mudofaa stsenariylarini simulyatsiya qiladi, shu bilan birga o'qitish va ish jarayonini optimallashtirishni qo'llab-quvvatlaydi. 

---

## **Tarmoq topologiyasi**
Laboratoriya tarmog'i xavfsizlik va ko'p qirralilik uchun tuzilgan.

```
┌─────────────────────────────────────────────────────────┐
│                        [ WAN ]                          │
│                           ▲                             │
│                      ┌──────────┐                       │
│         ┌───[LAN]───►│ OPNsense │◄───[DMZ]───┐          │
│         │            └──────────┘            │          │
│         │                                    │          │
│         ▼                                    ▼          │
│ ┌───────────────┐                   ┌─────────────────┐ │
│ │   BlackArch   │                   │  Fedora Server  │ │
│ ├───────────────┤                   ├─────────────────┤ │
│ │     Arch      │                   │  HMVM Machines  │ │
│ ├───────────────┤                   └─────────────────┘ │
│ │ Ubuntu Server │                                       │
│ └───────────────┘                                       │
└─────────────────────────────────────────────────────────┘
```

---

## **Qisqacha Tavsilotlar**
 
### OPNsense
- Kiruvchi va chiquvchi trafikni boshqaruvchi **xavfsizlik devori** va **asosiy router** bo'lib xizmat qiladi.
- Izolyatsiya va boshqariladigan kirishni ta'minlash uchun ichki va tashqi tarmoqlarni segmentlarga ajratadi.
- Avtomatik IP tayinlash uchun **DHCP** beradi.
- Xavfsiz masofaviy kirish uchun ixtiyoriy **VPN**-ni qo'llab-quvvatlaydi.

### [LAN] – Ishonchli tarmoq
- Ishonchli mashinalarni o'z ichiga oladi.
- Ochiq internetdan cheklanmagan foydalanish imkoniyatiga ega.

#### BalckArch _(Asosiy mashina)_
- **kirish testi** va **ekspluatatsiyani rivojlantirish** uchun asosiy hujumkor xavfsizlik Sistemasi.

#### Arch Linux _(Qo'shimcha Kvest)_
- **Linux ricing** uchun ishlatiladi.

#### Arch Server _(Asosiy Server)_
- **C2 ramkalar**, **veb-ilovalar** va **Eksploitlar**ni uchun host sifatida ishlatiladi.

### [DMZ] – Zaif tarmoq
- **ochiq internetga kirish imkoni yo'q**
- Sinov va amaliyot uchun zaif mashinalarni saqlaydi.

#### Fedora Server
- Amaliy ekspluatatsiyani ishlab chiqish uchun **maxsus zaifliklarni** taqlid qilish maqsadida ishlab chiqilgan.

#### HackMyVM Mashinalari
- Red Team va pentest amaliyoti uchun mo'ljallangan, oldindan qurilgan zaif mashinalar.

---

Note: Yes, `i use arch, BTW`