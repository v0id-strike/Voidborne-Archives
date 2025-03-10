#### Overview  
Configure VirtualBox networking and virtual machines (VMs) to create isolated lab environments.  

#### Steps:

1. Install VirtualBox  
   - Download from [VirtualBox.org](https://www.virtualbox.org/).  
   - Enable VT-x/AMD-V and Nested Virtualization in BIOS/UEFI.  

2. I use Cachy-OS, so i install it accordingly [here](CachyOS-Guide.md)

3. Create Virtual Networks
	- Go to File > Host Network Manager > Create. 
	- Trusted LAN:  
		- Go to File > Host Network Manager > Create.  
		- Name: vboxnet0 
		- IPv4: 192.168.56.1/24
		- DHCP: Disabled.  
	- Isolated Lab:  
	    - Name: isolated-lab 
	    - IPv4: 192.168.57.1/24 
	    - DHCP: Disabled.  

4. VMs: 
- VM Specs

| VM                                | RAM  | CPU | Storage | Adapter 1    | Adapter 2    |
| --------------------------------- | ---- | --- | ------- | ------------ | ------------ |
| [OpnSense](OpnSense.md)           | 4GB+ | 2+  | 40GB+   | NAT (WAN)    | vtnet0 (LAN) |
| [AthenaOS](AthenaOS.md)           | 4GB+ | 2+  | 100GB+  | vtnet0 (LAN) | -            |
| [Arch](Arch.md)                   | 2GB+ | 2+  | 50GB+   | vtnet0 (LAN) | -            |
| [Ubuntu-Server](Ubuntu-Server.md) | 2GB+ | 2+  | 50GB+   | vtnet0 (LAN) | -            |
| [Fedora-Server](Fedora-Server.md) | 2GB+ | 2+  | 20GB+   | vtnet1 (DMZ) | -            |
| Windows                           | 4GB+ | 2+  | 80GB+   | vtnet1 (DMZ) | -            |
| Sub-Targets                       |      |     |         | vtnet1 (DMZ) | -            |

- Network Topology 
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

- Connection Breakdown
	- Internet → OpnSense: Acts as the firewall and main router, controlling network access.
	- OpnSense → Internal VMs: 
		- Provides DHCP for automatic IP assignments.
		- Firewall Rules allow or block traffic between different networks.
		- VPN (Optional) for remote access.
	- Windows (Active Directory):
		- Used for Privilege Escalation and AD Exploits.
		- Can be attacked from AthenaOS or Ubuntu Server.
	- Server:
		- Hosts C2 Frameworks, Web Applications, or Exploit Development.
	- AthenaOS:
		- Main Offensive Security VM (used for pentesting & exploitation).
		- Can attack Windows & Metasploitable.
	- VulnerableVMs:
		- Purposely vulnerable systems for practicing exploits.
