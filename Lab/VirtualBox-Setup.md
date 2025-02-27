#### Overview  
Configure VirtualBox networking and virtual machines (VMs) to create isolated lab environments.  

#### Steps:

1. Install VirtualBox  
   - Download from [VirtualBox.org](https://www.virtualbox.org/).  
   - Enable VT-x/AMD-V and Nested Virtualization in BIOS/UEFI.  

2. I use Cachy-OS, so i install it accordingly [here](Lab/CachyOS-Guide)

3. Create Virtual Networks  
- Trusted LAN:  
	- Go to File > Host Network Manager > Create.  
	- Name: trusted-lan, IPv4: 192.168.56.1/24, DHCP: Disabled.  
- Isolated Lab:  
    - Name: isolated-lab, IPv4: 192.168.57.1/24, DHCP: Disabled.  

1. VM List & Network Adapters  

| VM                       | RAM  | CPU | Storage | Adapter 1        | Adapter 2        |
| ------------------------ | ---- | --- | ------- | ---------------- | ---------------- |
| [OpnSense](Lab/OpnSense) | 4GB+ | 2+  | 40GB+   | Bridged (WAN)    | PublicNet (LAN)  |
| AthenaOS                 | 4GB+ | 2+  | 100GB+  | PublicNet (LAN)  | -                |
| Ubuntu Server            | 2GB+ | 2+  | 30GB+   | PublicNet (LAN)  | -                |
| Windows                  | 4GB+ | 2+  | 80GB+   | PublicNet (LAN)  | PrivateNet (DMZ) |
| Metasploitable 3         | 5GB+ | 2+  | 70GB+   | PrivateNet (DMZ) | -                |
| Sub-Targets              |      |     |         | PrivateNet (DMZ) | -                |

5. Enable Nested Virtualization  
- For Windows/AthenaOS VMs:  
```bash
VBoxManage modifyvm "VM Name" --nested-hw-virt on
```
