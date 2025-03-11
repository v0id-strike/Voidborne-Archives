Got it! Since you're already on CachyOS and have an empty Btrfs partition, we'll install Arch on it while keeping your existing system intact.

---

## **🛠 Steps to Install Arch on the Empty Btrfs Partition**
### **1️⃣ Prepare the Partition**
First, check your partition table:

```bash
lsblk -f
```
- Identify the **empty Btrfs partition** (e.g., `/dev/nvme1n1pX`).
- If needed, format it (but since it’s already Btrfs, this step may not be necessary).

To format (only if required):
```bash
sudo mkfs.btrfs -f /dev/nvme1n1pX
```

---

### **2️⃣ Mount the Partition**
Create a mount point and mount the partition:

```bash
sudo mkdir -p /mnt/arch
sudo mount /dev/nvme1n1pX /mnt/arch
```

---

### **3️⃣ Bootstrap Arch Linux**
Use `pacstrap` to install the base system:

```bash
sudo pacstrap /mnt/arch base linux linux-firmware btrfs-progs
```

---

### **4️⃣ Generate fstab**
Generate an `fstab` file to ensure proper mounting:

```bash
sudo genfstab -U /mnt/arch | sudo tee /mnt/arch/etc/fstab
```

---

### **5️⃣ Chroot into the New Arch System**
Change root into the Arch installation:

```bash
sudo arch-chroot /mnt/arch
```

---

### **6️⃣ Set Up Basic Configuration**
Set the hostname:
```bash
echo "arch-btrfs" > /etc/hostname
```

Set up the locale:
```bash
echo "en_US.UTF-8 UTF-8" > /etc/locale.gen
locale-gen
echo "LANG=en_US.UTF-8" > /etc/locale.conf
export LANG=en_US.UTF-8
```

Set the root password:
```bash
passwd
```

---

### **7️⃣ Install GRUB for Dual Boot**
Since CachyOS is already using GRUB, we’ll add Arch to it.

Install GRUB inside Arch:
```bash
pacman -S grub efibootmgr
```

Find your EFI partition (likely `/dev/nvme1n1p1`) and mount it:
```bash
mount /dev/nvme1n1p1 /boot
```

Then install GRUB:
```bash
grub-install --target=x86_64-efi --efi-directory=/boot --bootloader-id=GRUB
grub-mkconfig -o /boot/grub/grub.cfg
```

---

### **8️⃣ Exit Chroot & Reboot**
Exit the chroot environment:
```bash
exit
```

Unmount the partitions:
```bash
sudo umount -R /mnt/arch
```

Reboot:
```bash
sudo reboot
```

After reboot, Arch should appear in the GRUB menu alongside CachyOS. 🚀 