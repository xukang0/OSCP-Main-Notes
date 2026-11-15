
[[Current Affairs Notes Template]]

---
# Steps to Gyoza

### User flag

nmap scan preliminarily shows evil win rm open. Enumerate that first while waiting

nxc-sweep tells us machine name is gyoza and winrm shows pwned

evilwinrm in and find SeImpersonatePrivilege, SharpEfsPotato for NT authority.

Flag on chen desktop

### Root flag

Flag on Administrator desktop

### Pivoting

Try to run sharphound. Succeeds. Found out domain name is poseidon.yzx

gyoza is sub.poseidon.yzx.

add info to /etc/hosts

in mimikatz secretsdump i see 

Secret  : _SC_SNMPTRAP / service 'SNMPTRAP' with username : sub\lisa
cur/text: LisaWayToGo456

also

DefaultPW
Impossible2Crack4.?

gyoza admin hash : 55525fffcb61c0b3765bf27fe521f630

Lisa creds authenticates onto .162

Lisa only has RDP no WInRM

nxc sweep Impossible2Crack4.? as well no matches

nxc tells us .162 is called dc02

---

# Steps to MS02 

### User flag




### Root flag



# Steps to DC01

### User flag



### Root flag




---

# Steps to Frankfurt
### User flag



### Root flag

---
# Steps to Charlie
### User flag



### Root flag



---
# Steps to Pascha
### User flag



### Root flag






