## **🛠 Arch Linux’ni Bo‘sh Btrfs Bo‘limiga O‘rnatish Bosqichlari**

### **1️⃣ Bo‘limni Tayyorlash**
Avvalo bo‘limlar jadvalini tekshiring:
```bash
lsblk -f
```
- Bo‘sh Btrfs bo‘limini aniqlang (masalan, /dev/nvme1n1pX).
- Agar kerak bo‘lsa, uni formatlang (lekin agar allaqachon Btrfs bo‘lsa, bu kerak emas).

Formatlash uchun (faqat zarurat bo‘lsa):
```
sudo mkfs.btrfs -f /dev/nvme1n1pX
```
---
### 2️⃣ **Bo‘limni Ulash**
Ulash nuqtasini yarating va bo‘limni ulang:
```
sudo mkdir -p /mnt/arch
sudo mount /dev/nvme1n1pX /mnt/arch
```
---
### 3️⃣ **Arch Linux’ni Bootstrap Qilish**
`pacstrap` yordamida tizimning asosiy komponentlarini o‘rnating:
```
sudo pacstrap /mnt/arch base linux linux-firmware btrfs-progs
```
---
### 4️⃣ **fstab Faylini Yaratish**
Bo‘limlar avtomatik ulanib turishi uchun `fstab` faylini yarating:
```
sudo genfstab -U /mnt/arch | sudo tee /mnt/arch/etc/fstab
```
---
### 5️⃣ **Arch Tizimiga Chroot Qilish**
Arch tizimiga o‘tish (chroot qilish):
```
sudo arch-chroot /mnt/arch
```
---
### 6️⃣ **Asosiy Sozlamalarni Amalga Oshirish**
Kompyuter nomini belgilang:
```
echo "arch-btrfs" > /etc/hostname
```
---
Til va kodlash tizimini sozlang:
```
echo "en_US.UTF-8 UTF-8" > /etc/locale.gen
locale-gen
echo "LANG=en_US.UTF-8" > /etc/locale.conf
export LANG=en_US.UTF-8
```
Root foydalanuvchi uchun parol o‘rnating:
```
passwd
```
---
### 7️⃣ **GRUB Yuklovchini O‘rnatish (Dual Boot Uchun)**
CachyOS allaqachon GRUB yuklovchidan foydalangani sababli, biz Arch Linux’ni unga qo‘shamiz.

Arch ichida GRUB’ni o‘rnating:
```
pacman -S grub efibootmgr
```
EFI bo‘limni aniqlang (odatda `/dev/nvme1n1p1`) va uni ulang:
```
mount /dev/nvme1n1p1 /boot
```
GRUB’ni o‘rnating:
```
grub-install --target=x86_64-efi --efi-directory=/boot --bootloader-id=GRUB
grub-mkconfig -o /boot/grub/grub.cfg
```
### 8️⃣ **Chroot’dan Chiqish va Qayta Yuklash**
Chroot muhitidan chiqing:
```
exit
```
Bo‘limlarni ajrating:
```
sudo umount -R /mnt/arch
```
Kompyuterni qayta yuklang:
```
sudo reboot
```
