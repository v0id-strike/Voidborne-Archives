Arch Linux tizimni sozlash ustidan toʻliq nazorat qilish imkonini beruvchi minimal, **DIY yondashuv** tufayli **ricing** uchun eng yaxshi tanlovdir. **O'zgaruvchan model** bilan Arch **zamonaviy dasturiy ta'minotni** va **AUR (Arch User Repository)** ga kirishni ta'minlaydi, bu uni maxsus mavzularni, oyna boshqaruvchilarini va tizim yordam dasturlarini o'rnatish va sozlash uchun mukammal qiladi. Uning **yengil tabiati** faqat sizga kerak bo'lgan komponentlar o'rnatilishini ta'minlaydi va tizimingizni **toza, tez va samarali** saqlaydi.

📥 Archni yuklash uchun [bu yerga](https://archlinux.org/download/).

---

## 📌 1-bosqich: Archni o'rnatish
### Live Boot
1. **ISO biriktiring** va Arch-ga yuklang
2. U **avtomatik tizimga kirishi kerak**
3. Saqlash moslamalarini tekshiring:
```bash
lsblk
```
_(Misol: Diskingiz `/dev/sda` deb faraz qilaylik)_

### Diskni bo'lish
1. `cfdisk`-ni ishga tushiring:
```bash
cfdisk /dev/sda
```
2. **GPT** bo'limini tanlang
3. Bo'limlarni yarating: 
	- **EFI bo'limi**: 
		- Hajmi: **512MB** 
		- Turi: **EFI tizimi** 
	- **Ildiz bo'limi**: 
		- Hajmi: **Qolgan joy** 
		- Turi: **Linux fayl tizimi**
4. **Write va Quit**

Bo'limlarni tekshiring:
```bash
lsblk
```

### Bo'limlarni formatlash
1. Format **EFI**:
```bash
mkfs.fat -F32 /dev/sda1
```
2. Format **Root (Btrfs)**:
```bash
mkfs.btrfs /dev/sda2
```

### Bo'limlarni yuklash
1. Root qismini o'rnatish:
```bash
mount /dev/sda2 /mnt
```
2. EFI bo'limini yarating va o'rnating:
```bash
mkdir /mnt/boot
mount /dev/sda1 /mnt/boot
```
3. Asosiy tizimni o'rnatish
```bash
pacstrap /mnt base linux linux-firmware vim networkmanager
```
4. fstab-ni yarating
```bash
genfstab -U /mnt >> /mnt/etc/fstab
```

### Tizimga Chroot bilan kiring
```bash
arch-chroot /mnt
```

- Vaqt mintaqasini o'rnating
```bash
ln -sf /usr/share/zoneinfo/Region/City /etc/localtime
hwclock --systohc
```
- Edit `/etc/locale.gen` and **uncomment**:
```
en_US.UTF-8 UTF-8
```
- Generate locale:
```bash
locale-gen
```
- Set default locale:
```bash
echo "LANG=en_US.UTF-8" > /etc/locale.conf
```
- Set Hostname
```bash
echo "myhostname" > /etc/hostname
```
- Edit `/etc/hosts`:
```
127.0.0.1  localhost
::1        localhost
127.0.1.1  myhostname.localdomain myhostname
```
- Root parolni o'rnating
```bash
passwd
```
- Bootloader-ni o'rnating
```bash
pacman -S grub efibootmgr
grub-install --target=x86_64-efi --efi-directory=/boot --bootloader-id=GRUB
grub-mkconfig -o /boot/grub/grub.cfg
```
- O'rnatishni tugatish
```bash
exit
umount -R /mnt
reboot
```

---

## 📌 2-bosqich: O'rnatishdan keyingi (qayta ishga tushirilgandan keyin)

- Root sifatida tizimga kiring, keyin:
- NetworkManager-ni yoqing:
```bash
systemctl enable NetworkManager
systemctl start NetworkManager
```
- Yangi foydalanuvchi yarating:
```bash
useradd -m -G wheel -s /bin/bash myuser
passwd myuser
```
- Sudo imtiyozlarini bering:
```bash
pacman -S sudo
echo "myuser ALL=(ALL) ALL" >> /etc/sudoers
```

---
## Yakuniy fikrlar
Siz laboratoriyangizda **Arch**-ni muvaffaqiyatli sozladingiz. 🔥
💡 Agar qoʻlda oʻrnatishdan qoʻrqsangiz 🚀 “archinstall” buyrugʻidan foydalaning