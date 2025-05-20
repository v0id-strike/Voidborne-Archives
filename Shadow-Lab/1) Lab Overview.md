## **Lab Purpose**

This lab is built for hands-on learning in Red Teaming, system administration, and Linux customization. It simulates real-world attack/defense scenarios while also supporting teaching and workflow optimization.

---

## **Network Topology**  
The Shadow-Lab network is structured for both security and versatility.  

```
┌─────────────────────────────────────────────────────────┐
│                        [ WAN ]                          │
│                           ▲                             │
│                      ┌──────────┐                       │
│         ┌───[LAN]───►│ OPNsense │◄───[DMZ]───┐          │
│         │            └──────────┘            │          │
│         │                                    │          │
│         ▼                                    ▼          │
│ ┌───────────────┐                   ┌─────────────────┐ │
│ │   BlackArch   │                   │  Fedora Server  │ │
│ ├───────────────┤                   ├─────────────────┤ │
│ │     Arch      │                   │  HMVM Machines  │ │
│ ├───────────────┤                   └─────────────────┘ │
│ │ Ubuntu Server │                                       │
│ └───────────────┘                                       │
└─────────────────────────────────────────────────────────┘
```

---

## **Simple Breakdown**  
 
### OPNsense

- Serves as the **firewall** and **primary router**, managing inbound and outbound traffic.
- Segments internal and external networks to ensure isolation and controlled access.
- Provides **DHCP** for automatic IP assignments.
- Supports an optional **VPN** for secure remote access.

### [LAN] – Trusted Network

- Hosts trusted machines.
- Has unrestricted access to the open internet.

#### BalckArch _(Main Machine)_

- Primary offensive security VM for **penetration testing** and **exploit development**.
- Targets vulnerable machines for real-world simulation.


#### Arch Linux _(Side Quest)_

- Used for **Linux ricing** and deep customization.
- Helps improve **workflow efficiency** and **aesthetic productivity**.

#### Arch Server _(Main Server)_

- Main server used to **teach my brother** and explore **system administration**.
- Hosts **C2 frameworks**, **web applications**, and **exploit development tools**.

### [DMZ] – Vulnerable Network

- Isolated segment with **no access to the open internet**.
- Hosts intentionally vulnerable machines for testing and practice.

#### Fedora Server

- Purpose-built to simulate **custom vulnerabilities** for hands-on exploit development.

#### HackMyVM Machines

- Pre-built vulnerable machines designed for Red Team and pentest practice.

---

Note: Yes, `i use arch, BTW`