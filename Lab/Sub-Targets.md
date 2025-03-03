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

You can convert the VMware Metasploitable 2 VM to VirtualBox using one of the following methods:  

---

### Method 1: Use VirtualBox to Directly Import VMDK
1. Extract the VM  
   - The Metasploitable 2 VM usually comes as a .zip file. Extract it.
   - Inside, you'll find a .vmdk file (VMware disk) and a .vmx file (VM configuration).

2. Create a New VM in VirtualBox  
   - Open VirtualBox and click New.
   - Name the VM (e.g., Metasploitable2).
   - Select Linux → Ubuntu (64-bit).
   - Assign 512MB or 1024MB RAM.

3. Use the Existing VMDK Disk  
   - When asked for a hard disk, choose "Use an existing virtual hard disk file".
   - Select the .vmdk file from the extracted folder.
   - Finish the VM setup.

4. Adjust VM Settings  
   - Go to Settings → System → Processor and enable PAE/NX.
   - In Network, set Adapter 1 to Bridged Adapter or Host-Only Adapter.

5. Start the VM  
   - Boot it up and log in with:
     
     Username: msfadmin
     Password: msfadmin
     

---

### Method 2: Convert VMDK to VDI (Optional)
If the VM does not boot correctly, convert the .vmdk disk to VirtualBox’s native format (.vdi).

1. Convert the Disk  
      VBoxManage clonehd "Metasploitable2.vmdk" "Metasploitable2.vdi" --format vdi
   

2. Attach the `.vdi` File  
   - Open VirtualBox.
   - Go to Settings → Storage.
   - Remove the old .vmdk disk.
   - Add the new .vdi disk.

3. Start the VM and it should work!

---

This should allow you to run Metasploitable 2 on VirtualBox without issues. Let me know if you hit any errors! 🚀