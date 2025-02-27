#### Overview  
Deploy intentionally vulnerable machines for practice.  

#### Steps  
1. Metasploitable 3  
   - Download from [Rapid7](https://github.com/rapid7/metasploitable3).  
   - Network: isolated-lab → 192.168.57.10/24.  

2. DVWA (Damn Vulnerable Web App)  
```bash   
docker run -d -p 80:80 vulnerables/web-dvwa  
```

   - Access via http://192.168.20.20.  

3. Isolation Rules  
   - Ensure no gateway/DNS is set on sub-targets.  
   - Test connectivity:  
```bash
ping 8.8.8.8  # Should fail  
```