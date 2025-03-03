#### Overview  
Deploy OPNsense as your lab’s firewall/router for network segmentation and security.
You can download ISO file from [OPNsense.org](https://opnsense.org/)

---
#### Steps 
1. Create OpnSense VM  
   - Name: OpnSense
   - Type: BSD
   - Subtype: FreeBSD
   - Version: FreeBSD (64-bit) 

2. Login to Live Boot
   - Attach installed ISO to VM
   - Login:  installer/opnsense
   - Choose Keymap
   - i recommend to install ZFS if your PC is decent
   - we are using Virtualbox, which is single disk, so choose stripe
   - Select disk by pressing `space` and `enter` to continue
   - choose `Yes` to confirm that you are ok with wiping out the disk
   - Now wait till installation is complete 

3. Initial Configuration  
   - Login: root/opnsense
   - In the console menu, select Option 1: Assign Interfaces  
    1. Set WAN to em0 (NAT)  
    2. Set LAN to em1 (192.168.56.1/24) 
    3. Set DMZ to em2 (192.168.57.1/24)
   -  Choose Option 2: Set Interface IP  
    1. Select LAN (em1)  
        - Assign IP: 192.168.56.2/24  
        - Do not set a gateway for LAN  
        - Enable DHCP: Yes (if you want OPNsense to assign IPs to your VMs)
        - Choose range between 192.168.56.10-200
    2. Select DMZ (em2)
        - Assign IP: 192.168.57.1/24  
        - Do not set a gateway for LAN  
        - Enable DHCP: Yes (if you want OPNsense to assign IPs to your VMs)
        - Choose range between 192.168.57.10 -> 200
   - Choose Option 12: Update from console

4. Enable Firewall & NAT in OPNsense
   - Access OPNsense Web GUI  
    1. Open a browser
    2. Go to: http://192.168.56.2  
    3. Login (root / opnsense)
    4. Follow to setup wizard
   - Enable NAT for Internet Access  
    1. Go to Firewall > NAT > Outbound  
    2. Select Hybrid mode  
    3. Add a rule:  
        - Interface: WAN  
        - Source: LAN Net  
        - Destination: Any  
        - Translation: Interface Address
        - Description: "Allow NAT for Internet Access"
    4. Click Apply Changes  
   - Add firewall rules for OPT1
    1.  Go to Firewall > Rules > OPT1
    2. Add a rule:  
        - Action: Pass
        - Protocol: Any  
        - Source: OPT1 net  
        - Destination: WAN  
        - Description: "Allow OPT1 to access Internet" 
    3. Add a rule:
        - Action: Block  
        - Protocol: Any  
        - Source: OPT1 net  
        - Destination: LAN net  
        - Description: "Block OPT1 from LAN access"  
    4. Click Save & Apply Changes    
   -  Add firewall rules for LAN  
    1. Go to Firewall > Rules > LAN  
    2. Add a rule:
        - Action: Pass  
        - Protocol: Any  
        - Source: LAN Net  
        - Destination: Any  
        - Description: "Allow LAN traffic"
    3. Add a rule:
        -  Action: Pass 
        - Protocol: TCP  
        - Source: LAN net  
        - Destination: OPT1 net  
        - Description: "Allow LAN to access OPT1"  
    4. Click Apply Changes  

5. Test Connectivity
   - Check if VMs get an IP  
   - Test Internet   
   - Check Firewall Logs:  
    1. Go to Firewall > Log Files > Live View  
    2. Look for blocked connections if internet isn't working. 
   - Try pinging LAN from DMZ (should be blocked).  
   - Try browsing the internet from DMZ (should work).  
   - Try accessing the web server in DMZ from LAN (should work).  
   - Try accessing the web server from the internet (if port forwarding is enabled).  

---
#### Quick Walkthrough  
You’ve built the fortress—now let’s arm it. This guide will transform you from a novice to a firewall warlord.  

**The Dashboard (Your War Room)  
- Key Widgets:  
  - Interfaces: Monitor WAN/LAN traffic.  
  - Gateway: Check internet connectivity.  
  - Firewall Logs: Spot intruders in real-time.  
- Customize: Drag/drop widgets to suit your style.  

**Interfaces (The Gates)**  
*WAN (The Outer Gate)*  
- Settings:  
  - IPv4 Configuration: DHCP (if your ISP provides it) or Static.  
  - Block Private Networks: Enable (stops RFC1918 traffic).  
  - Block Bogon Networks: Enable (stops invalid IP ranges).  
*LAN (The Inner Sanctum)*  
- Settings:  
  - IPv4 Address: 192.168.56.2/24 (default).  
  - DHCP Server: Enable (assigns IPs to your devices).  
*OPT1 (Optional Gate - DMZ)*  
- Settings:  
  - IPv4 Address: 192.168.57.1/24 (for vulnerable VMs).  
  - Firewall Rules: Block DMZ → LAN traffic.  

**Firewall Rules (The Siege Engines)**  
*WAN Rules*  
- Default: Block ALL inbound traffic.  
- Port Forwarding:  
  - Example: Forward WAN port 8080 → LAN IP 192.168.56.100:80.  
  - Path: Firewall > NAT > Port Forward.  
*LAN Rules*  
- Default: Allow ALL outbound traffic.  
- Harden Later: Block known malicious IPs using Firewall > Aliases.  
*OPT1 Rules*  
- Default: Allow LAN → DMZ (for testing).  
- Block: DMZ → LAN (isolate vulnerable VMs).  

**Services (The Arsenal)**
*DHCP Server*  
- Path: Services > DHCPv4 > LAN.  
- Range: 192.168.56.10 - 192.168.56.200.  
- DNS: 1.1.1.1 (Cloudflare) or 192.168.56.2 (OPNsense).  
*Suricata IDS/IPS*  
- Path: Services > Intrusion Detection > Administration.  
- Enable: On WAN and LAN.  
- Rulesets: Download ET Open Ruleset (free).  
- Blocklists: Add known malicious IPs.  

*WireGuard VPN*  
- Path: Services > WireGuard.  
- Setup:  
  1. Add a Local endpoint (your OPNsense).  
  2. Add Peers (your devices).  
  3. Assign to an interface (e.g., LAN).  
- Use: Securely access your lab from anywhere.  

**System (The Keep)** 
*Firmware Updates*
- Path: System > Firmware > Update.  
- Check Regularly: Patch vulnerabilities.  
*Backup/Restore*  
- Path: System > Configuration > Backups.  
- Download: Save your config (opnsense-config.xml).  
- Upload: Restore after a disaster.  
*High Availability (Optional)*  
- Path: System > High Availability.  
- Use: Sync two OPNsense firewalls for failover.  

**Monitoring (The Watchtower)**  
*Firewall Logs* 
- Path: Firewall > Log Files > Live View.  
- Use: Spot attacks in real-time.  
*Traffic Graphs*  
- Path: Interfaces > Interface > Graphs.  
- Use: Monitor bandwidth usage.  
*Reporting*  
- Path: Reporting > NetFlow.  
- Use: Analyze traffic patterns.  

**Advanced Tactics**  
*Captive Portal*  
- Path: Services > Captive Portal.  
- Use: Force authentication for guest Wi-Fi.  
*Traffic Shaping*  
- Path: Firewall > Traffic Shaper.  
- Use: Prioritize critical traffic (e.g., VoIP).  
*HAProxy (Load Balancer)*  
- Path: Services > HAProxy.  
- Use: Distribute traffic across multiple servers.  

**Practice Scenarios** 
1. Port Forwarding: Expose a web server in your DMZ.  
2. VPN Setup: Connect to your lab remotely via WireGuard.  
3. IDS/IPS Testing: Trigger Suricata with a simulated attack (e.g., nmap -sV).  

**Resources**  
- Official Docs: [OPNsense Documentation](https://docs.opnsense.org/).  
- Forums: [OPNsense Community](https://forum.opnsense.org/).  
- YouTube: Search for "OPNsense Tutorials" (e.g., by Lawrence Systems).  

**Final Words**  
OPNsense is your sword and shield. Master it, and no network will defy you.
*(P.S. Reward yourself. Even firewall warlords need coffee.* ☕️)
