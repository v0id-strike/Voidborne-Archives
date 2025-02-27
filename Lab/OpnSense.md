#### Overview  
Deploy OPNsense as your lab’s firewall/router for network segmentation and security.  

#### Steps 
1. Install OPNsense  
   - Download the ISO from [OPNsense.org](https://opnsense.org/).  
   - Attach the ISO to an OpnSense VM.  

2. Initial Configuration  
   - Assign interfaces during setup:  
     - WAN: vtnet0 (Bridged to host’s physical NIC).  
     - LAN: vtnet1 (Trusted LAN: 192.168.56.1/24).  

3. Enable NAT & DHCP  
   - Services > DHCPv4 > LAN:  
     - Range: 192.168.56.100-200.  
   - Firewall > NAT > Outbound: Enable Hybrid Outbound NAT.  

4. Firewall Rules  
   - WAN: Block all inbound traffic by default.  
   - LAN: Allow all outbound traffic.  

5. Enable Suricata IDS  
   - Services > Intrusion Detection > Administration:  
     - Enable on WAN interface.  
     - Download ET Open ruleset.  
