### Initial Domain Enumeration
#### Domain users
```
nxc smb <DC_IP> -u USER -p PASS --users
```
#### Domain groups
```
nxc smb <DC_IP> -u USER -p PASS --groups
```
#### Shares
```
nxc smb <DC_IP> -u USER -p PASS --shares
```
#### LDAP users
```
nxc ldap <DC_IP> -u USER -p PASS --users
```
#### LDAP computers
```
nxc ldap <DC_IP> -u USER -p PASS --computers
```
#### Password policy
```
nxc smb <DC_IP> -u USER -p PASS --pass-pol
```
#### Domain information
```
nxc smb <DC_IP> -u USER -p PASS
```
