## 🔹 Step 0 — Identify Architecture

### Linux

```
uname -m
```

- `x86_64` → amd64
- `aarch64` → arm64
### Windows

**CMD**

```cmd
systeminfo | findstr /i "System Type
```

**PowerShell**

```powershell
$env:PROCESSOR_ARCHITECTURE
```

> ⚠️ Always match **agent/proxy binary architecture** to the target.

---