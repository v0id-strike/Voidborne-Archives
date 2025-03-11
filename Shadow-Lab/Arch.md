#### Overview  
Why it is here, just to test(*taste*) my rices
You can download ISO file from [here](https://archlinux.org/download/)

#### Steps  
1. Create Arch VM  
   - Name: Arch
   - Type: Linux
   - Subtype: Archlinux
   - Version:  Archlinux (64-bit)

2. Login to Live Boot
   - Attach installed ISO to VM
   - Login:  auto-login
   - Type `lsblk` to get storage names. (i get 'sda' for my 50GB storage)
   - `cfdisk /dev/sda`
   - Select `GPT`
   - Create Partitions:
	   1. EFI Partition:
		   - Size: 512MB
		   - Type: EFI System
	   2. Root Partition:
		   - Size: Remaining space (~49.5GB)
		   - Type: Linux filesystem
		   - Write: yes
   - rerun `lsblk` to check if changes are applied
   - Format partitions:
	   1. `mkfs.fat -F32 /dev/sda1`
	   2. `mkfs.btrfs /dev/sda2`
   - Mount partitions:
	   1. `mount /dev/sda2 /mnt`
	   2. `mkdir /mnt/boot`
	   3. `mount /dev/sda1 /mnt/boot`
   - Install base system:
	   1. `pacstrap /mnt base linux linux-firmware vim networkmanager`
	   2. `genfstab -U /mnt >> /mnt/etc/fstab`
	   3. `arch-chroot /mnt`
   - Configure system:
	   1. set timezone:
		   - `ln -sf /usr/share/zoneinfo/Region/City /etc/localtime`
		   - `hwclock --systohc`
	   2. Localization:
		   - Edit /etc/locale.gen and uncomment your locale (e.g., en_US.UTF-8 UTF-8).
		   - `locale-gen`
		   - `echo "LANG=en_US.UTF-8" > /etc/locale.conf`
	   3. Network Configuration:
		   - `echo "myhostname" > /etc/hostname`
		   - Edit `/etc/hosts`
			   1. `127.0.0.1  localhost`
			   2. `::1        localhost`
			   3. `127.0.1.1  myhostname.localdomain myhostname`
	   4. Set root password
		   - `passwd` 
	   5. Install bootloader
		   - `pacman -S grub efibootmgr`
		   - `grub-install --target=x86_64-efi --efi-directory=/boot --bootloader-id=GRUB`
		   - `grub-mkconfig -o /boot/grub/grub.cfg`
	   6. Finish
		   - `exit`
		   - `umount -R /mnt`
		   - `reboot`
   - And if your system boots up. good luck with Arch journey.
   - For me, looks like i screwed up in some place. (i am teaching my club with [Ubuntu-Server](Ubuntu-Server.md) 😞)