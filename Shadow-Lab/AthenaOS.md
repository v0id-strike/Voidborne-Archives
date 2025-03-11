AthenaOS is a **lightweight, Arch-based** penetration testing distribution that integrates **BlackArch** repositories, providing access to cutting-edge security tools. Unlike Kali or Parrot, it leverages **rolling updates, superior package management (pacman), and high customizability** while remaining lightweight enough to run on older hardware.

📥 **Download AthenaOS**: [athenaos.org](https://athenaos.org/)

---

## **📌 Phase 1: Creating the AthenaOS VM**

### **1️⃣ Setup Virtual Machine**

1. Open **VirtualBox** and click **New**.
2. Name the VM: **AthenaOS**
3. Type: **Linux**
4. Version: **Arch (64-bit)**
5. VirtualBox Settings > Display
	-  Increase **VRAM to 128MB**
6. VirtualBox Settings > Network:
    - **Adapter 1:** Attached to: **Host-only Adapter**

---

## **📌 Phase 2: Installing AthenaOS**

### **2️⃣ Boot into Live Environment**

1. Attach the **AthenaOS ISO** to the VM.
2. Start the VM; it **auto-logs into the live session**.
3. The **Athena Welcome Window** appears.

### **3️⃣ Install AthenaOS (TUI Installer)**

1. Click **"Update Mirrors"**, wait for updates.
2. Select **"Install Athena OS (TUI)"**.
3. Choose **"Athena Arch"**, then confirm with **"Yes"**.
4. Set up system preferences:
    - **Timezone:** Select your region.
    - **Console Keymap:** (e.g., `en`)
    - **GUI Keymap:** (e.g., `us`)
    - **Locale:** (e.g., `en_US.UTF-8 UTF-8`)
5. Enter user credentials:
    - **Username & Password**
    - **Root Password**
    - **Hostname**
6. **Partitioning**
    - Choose **"Automatic"** (if unsure).
    - Select the **disk to partition**.
    - Create a **swap partition** if needed.
7. **Customize System**
    - **Desktop Environment**: Choose **Gnome/ KDE / XFCE / i3/.....**.
    - **Shell**: Choose **zsh / bash / fish**.
    - **Theme**: [Overall Themes](https://athenaos.org/en/configuration/themes/).
    - **Browser**: Firefox / Brave.
    - **Display Manager**: [SDDM themes](https://athenaos.org/en/configuration/display-manager/).
    - **Terminal Emulator**: Alacritty / Konsole / Kitty /.......
8. **Enable Additional Features**:
    - ✅ **IPv6** (if needed)
    - ✅ **Flatpak** (for additional apps)
    - ❌ **ZRAMD** (Disable if swap is created)
9. Confirm and **start installation**.
10. Once complete, **reboot** the VM.

---

## **📌 Phase 3: Post-Installation Setup**

### **4️⃣ Setup Cybersecurity Role**

1. Login to AthenaOS.
2. The **Athena-Welcome** screen appears.
3. **Top-right menu > Select Cyber Role**.
4. Click **"Set Cyber Role"** → This downloads and installs the **necessary pentesting tools** based on your role.

---

## **📌 Phase 4: Essential Security Tools**

### **5️⃣ Install Additional Pentesting Tools**

If you prefer to keep your system light, install security tools manually:

📌 **Updating System**

```bash
sudo pacman -Syu   # Update system
```

📌 **Common Pentesting Tools**

```bash
sudo pacman -S nmap metasploit hydra john sqlmap wireshark-cli wireshark-qt
```

📌 **Wireless & Bluetooth Hacking**

```bash
sudo pacman -S aircrack-ng reaver-wps-fork-t6x bettercap hcxdumptool hcxtools
```

📌 **Reverse Engineering & Exploitation**

```bash
sudo pacman -S gdb python-pwntools radare2 binwalk ghidra
```

📌 **Web Application Security**

```bash
sudo pacman -S burpsuite wfuzz zaproxy
```

📌 **Forensics & OSINT**

```bash
sudo pacman -S volatility recon-ng
```

---

## **📌 Phase 5: Testing & Monitoring**

### **🔹 Network Testing**

- Check if **AthenaOS can access the internet** (`ping google.com`).
- Test connectivity to **DMZ & LAN** VMs.

### **🔹 Penetration Testing Practice**

- **Target:** Metasploitable in **DMZ**.
- **Attack:** Run **nmap** and **Metasploit** scans.

```bash
nmap -p- -A 192.168.57.1/24
msfconsole
use exploit/unix/ftp/vsftpd_234_backdoor
```

### **🔹 System Monitoring**

- Monitor **network traffic**:

```bash
sudo tcpdump -i any
```

- Check **running processes**:

```bash
htop
```

---

## **Final Thoughts**

You’ve successfully set up **AthenaOS as a Red Team machine** in your home lab. 🔥
💡 **Unixporn + Arch + BlackArch = A Cybersecurity Beast!** 🚀