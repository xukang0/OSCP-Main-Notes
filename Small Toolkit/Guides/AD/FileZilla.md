FileZilla stores connection information in XML configuration files.

**Common locations:**
```
%APPDATA%\FileZilla\recentservers.xml
%APPDATA%\FileZilla\sitemanager.xml
%APPDATA%\FileZilla\filezilla.xml
```

**Enumerate all three:**
```
$paths = @(
    "$env:APPDATA\FileZilla\recentservers.xml",
    "$env:APPDATA\FileZilla\sitemanager.xml",
    "$env:APPDATA\FileZilla\filezilla.xml"
)

foreach ($path in $paths) {
    if (Test-Path $path) {
        Write-Host "`n===== $path ====="
        Get-Content $path
    }
}
```

Look for:
- `Host`
- `Port`
- `User`
- `Pass`
- `Protocol`

FileZilla passwords may be stored as plaintext, base64-encoded text, or using other protection depending on the version and storage settings.