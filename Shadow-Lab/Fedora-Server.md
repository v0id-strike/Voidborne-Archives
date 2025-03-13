Not all targets—like **DVWA (Damn Vulnerable Web App)**—come with an ISO. Instead, they need to be deployed using **Docker** or other containerization platforms.
By setting up a **Fedora Server VM**, we create a **powerful and stable environment** for hosting **vulnerable containers**, running **web services**, and managing **self-hosted applications**.

📥 Get the **Fedora Server ISO** from [here](https://fedoraproject.org/server/).

---

## **📌 Phase 1: Creating the Fedora VM**
### **1️⃣ Setup Virtual Machine**

1. Open **VirtualBox** and click **New**.
2. Name the VM: **Fedora Server**
3. Type: **Linux**
4. Version: **Fedora (64-bit)**
5. VirtualBox Settings > Network:
    - **Adapter 1:** Attached to: **Host-only Adapter**

---

## **📌 Phase 2: Installing AthenaOS**
### **2️⃣ Boot into Live ISO**

- Attach the **Fedora Server ISO** to your VM
- Start the **installer**

### **3️⃣ Installation Process**

- **Language & Keyboard:** Choose your preferred settings
- **Installation Destination:** Select the disk for installation
- **Time Zone:** Set your system time zone
- **User Accounts:**
    - Create a **root password**
    - Add a **regular user account** (recommended)
- **Begin Installation**
- Wait for the installation to complete
- **Reboot** into your newly installed Fedora Server