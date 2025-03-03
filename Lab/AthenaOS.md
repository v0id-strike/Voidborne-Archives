#### Overview  
Set up AthenaOS (Arch-based) for penetration testing and red teaming. 
You can download ISO file from [AthenaOS.org](https://athenaos.org/)

---
#### Steps  
1. Create AthenaOS VM  
   - Name: AthenaOS
   - Type: Linux
   - Subtype: Arch
   - Version: Arch (64-bit) 

2. Login to Live Boot
   - Attach installed ISO to VM
   - Login:  no-need (auto-login)
   - You will see Athena Welcome window:
	   1. Choose "Update Mirrors", wait
	   2. Choose "Install Athena OS (TUI)"
	   3. Choose "Athena Arch", and then "Yes"
	   4. Select a timezone
	   5. Select a console keymap (e.g. en)
	   6. Select GUI keymap (e.g. us)
	   7. Select a locale (e.g. en_US.UTF-8 UTF-8)
	   8. Type username, password, root password, hostname
	   9. Choose a partitioning mode
	   10. Select the disk to partition
	   11. Create a swap partition if needed
	   12. Choose desktop, shell, theme, browser, display manager, terminal to use
	   13. Enable ipv6, zramd, and/or flatpak if needed (don't enable if you created a swap)
	   14. Choose "Yes"
   - Now wait till installation is complete 

- Network Configuration  
```bash   
sudo ip addr add 192.168.56.10/24 dev eth0  
sudo ip route add default via 192.168.56.1  
echo "nameserver 8.8.8.8" | sudo tee /etc/resolv.conf  
```

- Install Tools  
```bash
sudo pacman -Syu  
sudo pacman -S metasploit nmap burpsuite crackmapexec  
```

- Configure SSH Access  
```bash
sudo systemctl enable --now sshd  
sudo passwd athena  # Set password  
```