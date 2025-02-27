Ah, the infamous `/dev/vboxnetctl` error! Fear not – this is common when setting up VirtualBox on Arch/CachyOS. Let's fix it step-by-step:

---

### **1. Install Required Packages**
Ensure you have **ALL** VirtualBox components:
```bash
sudo pacman -Sy virtualbox virtualbox-host-dkms virtualbox-guest-iso
```

---

### **2. Load Kernel Modules**
VirtualBox requires kernel modules to create virtual networks:
```bash
sudo modprobe vboxdrv vboxnetadp vboxnetflt
```

**Make modules load at boot**:
```bash
sudo tee /etc/modules-load.d/virtualbox.conf <<EOF
vboxdrv
vboxnetadp
vboxnetflt
EOF
```

---

### **3. Rebuild VirtualBox Kernel Modules**
This is **critical** if your kernel updated recently:
```bash
sudo vboxreload
```

---

### **4. Add User to `vboxusers` Group**
```bash
sudo usermod -aG vboxusers $USER
```
**Log out and back in** to apply group changes.

---

### **5. (Optional) Secure Boot Workaround**
If you use Secure Boot:
```bash
sudo pacman -S virtualbox-secureboot
sudo virtualbox-secureboot enroll
```
**Reboot** and enroll the key in your BIOS/UEFI.

---
### **Troubleshooting**
- **Kernel Headers Mismatch**? Ensure `linux-headers` matches your kernel:
  ```bash
  uname -r  # Check kernel version (e.g., 6.6.12-arch1-1)
  sudo pacman -S linux-headers
  ```
- Still broken? Nuke and rebuild:
  ```bash
  sudo rmmod vboxdrv vboxnetadp vboxnetflt
  sudo modprobe vboxdrv vboxnetadp vboxnetflt
  ```