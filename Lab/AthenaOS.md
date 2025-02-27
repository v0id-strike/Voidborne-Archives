#### Overview  
Set up AthenaOS (BlackArch-based) for penetration testing and red teaming.  

#### Steps  
1. Install AthenaOS  
   - Download ISO from [AthenaOS GitHub](https://github.com/Athena-OS/athena-iso).  
   - Create Athena VM.  

2. Network Configuration  
```bash   
sudo ip addr add 192.168.56.10/24 dev eth0  
sudo ip route add default via 192.168.56.1  
echo "nameserver 8.8.8.8" | sudo tee /etc/resolv.conf  
```

1. Install Tools  
```bash
sudo pacman -Syu  
sudo pacman -S metasploit nmap burpsuite crackmapexec  
```

4. Configure SSH Access  
```bash
sudo systemctl enable --now sshd  
sudo passwd athena  # Set password  
```