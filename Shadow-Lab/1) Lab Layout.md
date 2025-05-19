
## **Network Topology**  
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
# │ │   Athena OS   │                  |  Fedora Server  | |
# │ ├───────────────┤                  ├─────────────────┤ |
# │ │      Arch     │                  │  HMVM machines  │ │
# │ ├───────────────┼                  └─────────────────┘ │
# │ │ Ubuntu Server │                                      │
# │ └───────────────┘                                      │
# │                                                        │
# └────────────────────────────────────────────────────────┘
```

---

## **Simple Breakdown**  
 
- **OPNsense**  
  - Acts as the firewall and primary router, controlling inbound/outbound traffic.  
  - Segments internal and external networks, ensuring isolation and controlled access.  
  - Provides **DHCP** for automatic IP assignments.
  - Optional **VPN** for remote access.      

- **[LAN]** 
  - Trusted Machines Network
  - Has access to open internet

- **AthenaOS** (Main Machine)  
  - The primary offensive security VM for penetration testing and exploitation.  
  - Targets Vulnerable VMs for real-world attack simulation.  

- **Arch Linux**  (Side Quest)
  - Used for **Linux ricing** and customization.  
  - Helps refine **workflow efficiency** and visual aesthetics.  

- **Ubuntu Server** (Main Server)  
  - Primary server for **teaching my brother** and exploring system administration.  
  - Hosts **C2 frameworks, web applications, and exploit development tools**.  

- **[DMZ]**
  - Vulnerable Network
  - Holds target machines
  - Has no access to open internet

-  