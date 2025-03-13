The primary purpose of this VM is to serve as a **fortress of learning**—a place to **master Linux fundamentals**, **harden your sysadmin skills**, and **deploy web services** with confidence. Whether you're setting up a **self-hosted server**, **learning automation**, or **building a C2 framework**, this Ubuntu Server VM will be your **battle-tested** companion.

📥 Get the official **Ubuntu Server ISO** from [here](https://ubuntu.com/download/server).

---

## **📌 Phase 1: Creating the Ubuntu VM**
### **1️⃣ Setup Virtual Machine**

1. Open **VirtualBox** and click **New**.
2. Name the VM: **Ubuntu Server**
3. Type: **Linux**
4. Version: **Ubuntu (64-bit)**
5. VirtualBox Settings > Network:
    - **Adapter 1:** Attached to: **Host-only Adapter**

---

## **📌 Phase 2: Installing AthenaOS**
### **2️⃣ Boot into Live ISO**

- Attach the **Ubuntu ISO** to your VM
- Boot into **Ubuntu Installer**

### **3️⃣ Installation Process**

- **Language & Keyboard:** Choose your preferred settings
- **Network Setup:** Configure your network (can leave as default for DHCP)
- **Storage:** Choose **"Use entire disk"** (or manual partitioning if preferred)
- **User Account:**
    - Create a **username & password**
    - Set a hostname for your server
- **Additional Software (Optional):**
    - Tick **"Install OpenSSH server"** (important for remote access)
    - Select **third-party drivers** if prompted

### **4️⃣ Finish Installation**

- Start the installation process
- Once completed, **reboot** the system
- Login with your created user credentials