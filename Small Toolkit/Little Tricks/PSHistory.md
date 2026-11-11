```
powershell -ep bypass
```

```
Get-ChildItem C:\Users -Filter ConsoleHost_history.txt -Recurse -Force -ErrorAction SilentlyContinue |
ForEach-Object {
    Write-Host "`n========== $($_.FullName) ==========" -ForegroundColor Yellow
    Get-Content $_.FullName
}
```