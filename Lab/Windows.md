#### Overview  
Configure Windows as a dual-homed pivot host to reach isolated sub-targets.

#### Steps  
1. Install Windows VM  
   - Use [Windows 11 Evaluation ISO](https://www.microsoft.com/en-us/evalcenter/).   

2. Network Interfaces  
   - Adapter 1: trusted-lan → 192.168.56.100/24.  
   - Adapter 2: isolated-lab → 192.168.57.1/24.  

3. Enable IP Forwarding  
   - Open PowerShell as Admin:  

```powershell
Set-ItemProperty -Path "HKLM:\SYSTEM\CurrentControlSet\Services\Tcpip\Parameters" -Name "IPEnableRouter" -Value 1  
Restart-Computer
```

4. Disable Windows Defender  
```powershell  
Set-MpPreference -DisableRealtimeMonitoring $true  
```
   