Arch Linux is the ultimate choice for **ricing** due to its minimal, **DIY approach**, allowing complete control over system customization. With a **rolling-release model**, Arch provides **cutting-edge software** and access to the **AUR (Arch User Repository)**, making it perfect for installing and tweaking custom themes, window managers, and system utilities. Its **lightweight nature** ensures that only the components you need are installed, keeping your system **clean, fast, and efficient**—a dream setup for any ricer.

📥 Download **Arch ISO** from [here](https://archlinux.org/download/).

---

## 📌 Phase 1: Installing Arch
### Boot into Live Environment
1. **Attach ISO** and boot into Arch
2. It should **auto-login**
3. Check storage devices:
```bash
lsblk
```
_(Example: Assume your disk is `/dev/sda`)_

### Partition Disk
1. Run `cfdisk`:
```bash
cfdisk /dev/sda
```
2. Select **GPT** partitioning
3. Create partitions:
    - **EFI Partition**:
        - Size: **512MB**
        - Type: **EFI System**
    - **Root Partition**:
        - Size: **Remaining space**
        - Type: **Linux filesystem**
4. **Write & Quit**

Check partitions with:
```bash
lsblk
```

### Format Partitions
1. Format **EFI partition**:
```bash
mkfs.fat -F32 /dev/sda1
```
2. Format **Root partition (Btrfs)**:
```bash
mkfs.btrfs /dev/sda2
```

### Mount Partitions
1. Mount root partition:
```bash
mount /dev/sda2 /mnt
```
2. Create and mount EFI partition:
```bash
mkdir /mnt/boot
mount /dev/sda1 /mnt/boot
```
3. Install Base System
```bash
pacstrap /mnt base linux linux-firmware vim networkmanager
```
4. Generate fstab
```bash
genfstab -U /mnt >> /mnt/etc/fstab
```

### Chroot into System
```bash
arch-chroot /mnt
```

- Set Timezone
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
- Set Root Password
```bash
passwd
```
- Install Bootloader
```bash
pacman -S grub efibootmgr
grub-install --target=x86_64-efi --efi-directory=/boot --bootloader-id=GRUB
grub-mkconfig -o /boot/grub/grub.cfg
```
- Finish Installation
```bash
exit
umount -R /mnt
reboot
```

---

## 📌 Phase 2: Post-Installation (After Reboot)
- Login as root, then:
- Enable NetworkManager:
```bash
systemctl enable NetworkManager
systemctl start NetworkManager
```
- Create a new user:
```bash
useradd -m -G wheel -s /bin/bash myuser
passwd myuser
```
- Give sudo privileges:
```bash
pacman -S sudo
echo "myuser ALL=(ALL) ALL" >> /etc/sudoers
```

---
## Final Thoughts
You’ve successfully set up **Arch** in your home lab. 🔥
💡 Use `archinstall` command, if you afraid of manual installation 🚀