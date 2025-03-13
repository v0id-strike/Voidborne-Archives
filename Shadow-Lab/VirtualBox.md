Before building the Shadow-Lab, we first configure VirtualBox to suit our needs.  
There are many virtualization platforms available, but VirtualBox is one of the most widely used and beginner-friendly solutions. Its simplicity and cross-platform compatibility make it an excellent choice. However, if you are confident using other solutions and understand their configurations, feel free to experiment.  

---
#### **Install VirtualBox**  
- Download the latest version from [VirtualBox.org](https://www.virtualbox.org/).  
- Ensure **VT-x/AMD-V** and **Nested Virtualization** are enabled in BIOS/UEFI.  

---

#### **Create Virtual Networks**  
To establish proper network segmentation, we define two primary virtual networks:  

- **Trusted LAN (Internal Network for Core Machines)**  
  - Navigate to **File > Host Network Manager > Create**  
  - Name: `vboxnet0`  
  - IPv4 Address: `192.168.56.1/24`  
  - DHCP: **Disabled**  

- **Isolated Lab (DMZ for Vulnerable Machines)**  
  - Name: `vboxnet1`  
  - IPv4 Address: `192.168.57.1/24`  
  - DHCP: **Disabled**  

---

#### **Virtual Machine Specifications**  

| VM                                | RAM    | CPU    | Storage | Adapter 1    | Adapter 2    |
| --------------------------------- | ------ | ------ | ------- | ------------ | ------------ |
| [OPNsense](OpnSense.md)           | 4GB+   | 2+     | 40GB+   | NAT (WAN)    | vtnet0 (LAN) |
| [AthenaOS](AthenaOS.md)           | 8GB+   | 2+     | 100GB+  | vtnet0 (LAN) | -            |
| [Arch](Arch.md)                   | 2GB+   | 2+     | 50GB+   | vtnet0 (LAN) | -            |
| [Ubuntu-Server](Ubuntu-Server.md) | 2GB+   | 2+     | 50GB+   | vtnet0 (LAN) | -            |
| [Fedora-Server](Fedora-Server.md) | 2GB+   | 2+     | 20GB+   | vtnet1 (DMZ) | -            |
| [Targets](Targets.md)             | Varies | Varies | Varies  | vtnet1 (DMZ) | -            |

---

### **Network Topology**  
The Shadow-Lab network is structured for both security and versatility.  

```bash
#                       ┌───────────┐                       
# ┌─────────────────────│Virtual-Box│──────────────────────┐
# │                     └───────────┘                      │
# │                           ▲                            │
# │                         [WAN]                          │
# │                           ▼                            │
# │                      ┌─────────┐                       │
# │         ┌───[LAN]───►│Opn-Sense│◄───[DMZ]───┐          │
# │         │            └─────────┘            │          │
# │         │                                   │          │
# │         ▼                                   ▼          │
# │ ┌───────────────┐                  ┌─────────────────┐ │
# │ │   Athena OS   │                  │ Metasploitable2 │ │
# │ ├───────────────┤                  ├─────────────────┤ │
# │ │      Arch     │                  │  Fedora Server  │ │
# │ ├───────────────┼                  ├─────────────────┤ │
# │ │ Ubuntu Server │                  │   And  Others   │ │
# │ └───────────────┘                  └─────────────────┘ │
# │                                                        │
# └────────────────────────────────────────────────────────┘
```

---

### **Simple Breakdown**  

- **OPNsense**  
  - Acts as the firewall and primary router, controlling inbound/outbound traffic.  
  - Segments internal and external networks, ensuring isolation and controlled access.  
  - Provides **DHCP** for automatic IP assignments.
  - Optional **VPN** for remote access.      

- **AthenaOS (Attacker Machine)**  
  - The primary offensive security VM for penetration testing and exploitation.  
  - Targets Vulnerable VMs for real-world attack simulation.  

- **Arch Linux**  
  - Used for **Linux ricing** and customization.  
  - Helps refine **workflow efficiency** and visual aesthetics.  

- **Ubuntu Server**  
  - Primary server for **teaching my brother** and exploring system administration.  
  - Hosts **C2 frameworks, web applications, and exploit development tools**.  

- **Targets**  
  - Designed for **security testing and vulnerability exploitation**.    