#### Overview  
Host tools and command-and-control (C2) infrastructure.  

#### Steps  
1. Install Ubuntu Server  
   - Use the [Ubuntu 22.04 LTS](https://ubuntu.com/download/server) ISO.  
   - Minimal installation

2. Network Setup  
```bash
   sudo nano /etc/netplan/01-netcfg.yaml  
```

```yaml
network:
	version: 2
    ethernets:
	    eth0:
	        addresses: [192.168.56.20/24]
        routes:
	        - to: default
            via: 192.168.56.1
        nameservers:
	        addresses: [8.8.8.8]
```

```bash   
   sudo netplan apply  
```
