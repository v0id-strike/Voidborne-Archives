#### Overview  
Configure VirtualBox networking and virtual machines (VMs) to create isolated lab environments.  

#### Steps:

1. Install VirtualBox  
   - Download from [VirtualBox.org](https://www.virtualbox.org/).  
   - Enable VT-x/AMD-V and Nested Virtualization in BIOS/UEFI.  

2. I use Cachy-OS, so i install it accordingly [here](Lab/CachyOS-Guide)

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

| VM                       | RAM  | CPU | Storage | Adapter 1    | Adapter 2    |
| ------------------------ | ---- | --- | ------- | ------------ | ------------ |
| [OpnSense](Lab/OpnSense) | 4GB+ | 2+  | 40GB+   | NAT (WAN)    | vtnet0 (LAN) |
| AthenaOS                 | 4GB+ | 2+  | 100GB+  | vtnet0 (LAN) | -            |
| Server                   | 2GB+ | 2+  | 30GB+   | vtnet0 (LAN) | -            |
| Windows                  | 4GB+ | 2+  | 80GB+   | vtnet1 (DMZ) | -            |
| Sub-Targets              |      |     |         | vtnet1 (DMZ) | -            |

- Network Topology 
```bash
                          [Internet]  
                               │  
                       (NAT: VirtualBox)
                               │  
			 ┌────-─--─-───[OpnSense]──-───--─────┐
			 │             (Firewall)             │
			 │                                    │
	 [LAN: OpenNet]                       [DMZ: PrivateNet]
	 192.168.56.0/24                      192.168.57.0/24
			 │                                    │
┌───────--───┬───────--───┐          ┌──--────────┬─────--─────┐
│  AthenaOS  │  Server    │          │  VulnVM 1  │  VulnVM 2  │
│192.168.1.10│192.168.1.20│          │192.168.2.10│192.168.2.20│
└─────--─────┴─────--─────┘          └─────-──-───┴──-──-──────┘
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
