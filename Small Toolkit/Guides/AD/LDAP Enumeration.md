# Anonymous bind
```
ldapsearch -x -H ldap://DCIP -b "DC=domain,DC=htb"
```

# Authenticated
```
ldapsearch -x -H ldap://DCIP -D "user@domain.htb" -w 'password' -b "DC=domain,DC=htb"
```

# Find users
```
ldapsearch -x -H ldap://DCIP -D "user@domain.htb" -w 'pass' -b "DC=domain,DC=htb" "(objectClass=user)" sAMAccountName
```

# Find computers
```
ldapsearch -x -H ldap://DCIP -D "user@domain.htb" -w 'pass' -b "DC=domain,DC=htb" "(objectClass=computer)" name
```

# NetExec LDAP
```
nxc ldap DCIP -u user -p pass -d domain.htb --users
```

```
nxc ldap DCIP -u user -p pass -d domain.htb --groups
```
