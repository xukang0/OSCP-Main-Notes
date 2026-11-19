WinSCP can store saved sessions, usernames, server addresses and passwords.

**Registry enumeration (common default storage):**

```
reg query "HKCU\Software\Martin Prikryl\WinSCP 2\Sessions" /s
```

Look for:

- `HostName`
- `UserName`
- `PortNumber`
- `Password`
- `PrivateKeyFile`

**Check configuration files:**
```
Get-ChildItem "$env:APPDATA\WinSCP" -Force -Recurse -ErrorAction SilentlyContinue
```

Common configuration file:
```
%APPDATA%\WinSCP.ini
```

Read it:
```
Get-Content "$env:APPDATA\WinSCP.ini"
```

**Important:** WinSCP stored passwords may be encrypted/obfuscated. Don't assume the registry value is immediately a plaintext password.