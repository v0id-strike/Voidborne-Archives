## **Why OPNsense?**

In the realm of digital warfare, OPNsense stands as a formidable sentinel, balancing security, flexibility, and open-source freedom. It grants you the power to command your network, fortify your defenses, and orchestrate traffic with precision—an essential stronghold for any cybersecurity practitioner.

- Download the ISO from [OPNsense.org](https://opnsense.org/)

---
## **📌 Phase 1: Setting Up the OPNsense VM**

### **1️⃣ Create the Virtual Machine**

1. Open **VirtualBox** and click **New**.
2. Name the VM: **OPNsense**
3. Type: **BSD**
4. Version: **FreeBSD (64-bit)**
5. Allocate at least **1GB RAM** (2GB+ recommended).
6. Create a **10GB+ Virtual Hard Disk** (VDI, dynamically allocated).
7. Click **Settings > System**:
    - Enable **EFI** if using ZFS.
8. Go to **Network**:
    - **Adapter 1 (WAN)** → **Attached to NAT**
    - **Adapter 2 (LAN)** → **Attached to Internal Network (LAN)**
    - **Adapter 3 (DMZ)** → **Attached to Internal Network (DMZ)**

### **2️⃣ Install OPNsense**

1. Attach the OPNsense **ISO** to the VM and start it.
2. Login to live boot:
    - **Username:** `installer`
    - **Password:** `opnsense`
3. Select keyboard layout.
4. Choose **ZFS (Recommended for reliability)**.
5. Select **Stripe** (Single Disk).
6. Choose the installation disk and confirm wipe.
7. Once installed, **remove the ISO** and reboot.

---

## **📌 Phase 2: Initial Configuration**

### **3️⃣ Assign Network Interfaces**

1. Login: **root / opnsense**
2. Select **Option 1: Assign Interfaces**
    - **WAN** → `em0 (NAT)`
    - **LAN** → `em1 (vboxnet0)`
    - **DMZ** → `em2 (vboxnet1)`

### **4️⃣ Configure LAN & DMZ IPs**

1. Select **Option 2: Set Interface IP**
    
    - **LAN (em1):**
        - IP: `192.168.56.2/24`
        - No Gateway
        - Enable DHCP: **Yes** (`192.168.56.10 - 200`)
    - **DMZ (em2):**
        - IP: `192.168.57.1/24`
        - No Gateway
        - Enable DHCP: **Yes** (`192.168.57.10 - 200`)
2. Run **Option 12: System Update**.

---

## **📌 Phase 3: Configuring Firewall & NAT**

### **5️⃣ Access OPNsense Web GUI**

1. Open a browser.
2. Go to: `http://192.168.56.2`
3. Login: **root / opnsense**
4. Complete the setup wizard.
5. Rename **OPT1** to **DMZ** under **Interfaces**.

### **6️⃣ Enable NAT for Internet Access**

1. Go to **Firewall > NAT > Outbound**.
2. Select **Hybrid Mode**.
3. Create a **new rule**:
    - **Interface:** WAN
    - **Source Address:** LAN Net
    - **Destination:** Any
    - **Translation:** Interface Address
    - **Description:** `"Allow LAN Internet Access"`
4. Click **Apply Changes**.

### **7️⃣ Configure Firewall Rules**

#### **🛡️ DMZ Rules** (Firewall > Rules > DMZ)

✅ **Allow DMZ to Access Internet**

- Action: **Pass**
- Protocol: **Any**
- Source: **DMZ Net**
- Destination: **WAN Net**
- Click **Apply Changes**

🚫 **Block DMZ from Accessing LAN**

- Action: **Block**
- Protocol: **Any**
- Source: **DMZ Net**
- Destination: **LAN Net**
- Click **Apply Changes**

#### **🛡️ LAN Rules** (Firewall > Rules > LAN)

✅ **Allow LAN to Access the Internet**

- Action: **Pass**
- Protocol: **Any**
- Source: **LAN Net**
- Destination: **Any**
- Click **Apply Changes**

✅ **Allow LAN to Access DMZ**

- Action: **Pass**
- Protocol: **Any**
- Source: **LAN Net**
- Destination: **DMZ Net**
- Click **Apply Changes**

---

## **📌 Phase 4: Testing & Monitoring**

### **8️⃣ Verify Network Connectivity**

✅ Check if VMs receive an IP from DHCP.  
✅ Test **Internet access** from LAN & DMZ.  
✅ Ping **LAN from DMZ** (should be blocked).  
✅ Access a **DMZ web server from LAN** (should work).

### **9️⃣ Monitor Firewall & Logs**

1. Go to **Firewall > Log Files > Live View**.
2. Look for blocked connections.
3. Check **Interface Traffic Graphs** for bandwidth usage.

---

## **📌 Phase 5: Advanced Security Features**

### **🔐 Intrusion Detection (Suricata)**

1. Go to **Services > Intrusion Detection**.
2. Enable **IDS/IPS on WAN and LAN**.
3. Download **ET Open Ruleset**.

### **🛡️ VPN Access (WireGuard)**

1. Go to **Services > WireGuard**.
2. Add a **Local Endpoint** (your OPNsense).
3. Add **Peers** (remote devices).
4. Assign to **LAN Interface**.
5. Connect securely from anywhere.

### **🚨 Port Forwarding (Exposing Services)**

1. Go to **Firewall > NAT > Port Forward**.
2. Example: **Expose a DMZ Web Server**
    - **Interface:** WAN
    - **Destination:** WAN Address
    - **Port:** `8080 → 192.168.57.100:80`
    - Apply changes.
3. Test access from outside.

---

## **📌 Phase 6: Backup, Updates & High Availability**

### **🛠️ System Maintenance**

✅ **Regular Firmware Updates** (System > Firmware).  
✅ **Automated Backups** (System > Configuration > Backup).  
✅ **High Availability (HA)** (System > High Availability) to sync two OPNsense firewalls.