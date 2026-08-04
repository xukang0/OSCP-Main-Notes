## 🔹 Step 0 — Identify Architecture

### Linux

```
uname -m
```

- `x86_64` → amd64
- `aarch64` → arm64
### Windows

Run these two commands in your shell:

**PowerShell**

```powershell
C:\Windows\System32\WindowsPowershell\v1.0\powershell.exe -ep bypass
```

```powershell
powershell [Environment]::Is64BitOperatingSystem
```

```powershell
$env:PROCESSOR_ARCHITECTURE
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

- `x86_64` → amd64 → 32-bit
- `aarch64` → arm64 → 64 bit

> ⚠️ Always match **agent/proxy binary architecture** to the target.

---