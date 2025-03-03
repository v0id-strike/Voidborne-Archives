#### Overview  
Set up AthenaOS (BlackArch-based) for penetration testing and red teaming.  

#### Steps  
- Install AthenaOS  
   - Download ISO from [AthenaOS GitHub](https://github.com/Athena-OS/athena-iso).  
   - Create Athena VM.  

- Network Configuration  
```bash   
sudo ip addr add 192.168.56.10/24 dev eth0  
sudo ip route add default via 192.168.56.1  
echo "nameserver 8.8.8.8" | sudo tee /etc/resolv.conf  
```

- Install Tools  
```bash
sudo pacman -Syu  
sudo pacman -S metasploit nmap burpsuite crackmapexec  
```

- Configure SSH Access  
```bash
sudo systemctl enable --now sshd  
sudo passwd athena  # Set password  
```