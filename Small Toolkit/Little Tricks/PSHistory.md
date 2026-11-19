```
powershell -ep bypass
```

```
Get-Content (Get-PSReadLineOption).HistorySavePath
```

---

```
Get-ChildItem C:\Users -Filter ConsoleHost_history.txt -Recurse -Force -ErrorAction SilentlyContinue |
ForEach-Object {
    Write-Host "`n========== $($_.FullName) ==========" -ForegroundColor Yellow
    Get-Content $_.FullName
}
```

---

```
type C:\Users\*\AppData\Roaming\Microsoft\Windows\PowerShell\PSReadLine\ConsoleHost_history.txt
```

```
type C:\Users\leon\AppData\Roaming\Microsoft\Windows\PowerShell\PSReadLine\ConsoleHost_history.txt
```