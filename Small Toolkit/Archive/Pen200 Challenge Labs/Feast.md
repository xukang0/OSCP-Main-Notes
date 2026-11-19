
[[Current Affairs Notes Template]]

---
# Steps to MS01 

### Root flag

On nmap, found out domain name is feast.com. Add to /etc/hosts

Port 80 open on MS01. Investigate

192.168.245.170 shows cloudsync with a login page. Given creds allows login. 

Webpage runs php

There is hint of s3 aws bucket

Nmap scan on .168, then feroxbuster on port 80 reveals the aws s3 bucket

use [[AWS s3 bucket]] to get RCE

Land as nt authority MS01 and get flag on desktop

### Pivoting

Found alfpass123 in mimikatz

There is a passwords.txt in xampp

creds to mysql

Grant myself local RDP privilege.

RDP and finally able to access mysql

use cloudsync database and select * from users;

Gives several creds

john.doe       | 65fbef05e01fac390cb3fa073fb3e8cf : (MD5) anthony
jane.smith     | e99a18c428cb38d5f260853678922e03 : abc123
 bob.johnson    | 9fd8301ac24fb88e65d9d7cd1dd1b1ec : butterfly
 eric.wallows   | 179379cb0fc81ec454606fee56daa46e : None
 jeff.borrows   | cf9ee5bcb36b4936dd7064ee9b2f139e : naruto
  alice.williams | d914e3ecf6cc481114a3f534a5faf90b : andrew
  charlie.brown  | c03a5a4ba81cd3d8e59840a6f0eddad7 : tweety

Try to crackstation them first. Add them into users and passwords list. Nxc spray them

Only jeff.borrows:naruto works against dc01

nxc-sweep shows RDP available.doesnt work

Bloodhound shows jeff.borrows has genericall over mario lemieux. Directly change mario password.

Nxc-sweep mario across all services across all machines. MS02 pwned evilwinrm

---

# Steps to MS02 
### Root flag

whoami /groups shows mario.lemieux is a localadministrator.

flag on his desktop

### Pivoting

spotted BigFeast999! in mimikatz for administrator 6ab12784a390f4a54f0e240463587725

┌──(kali㉿kali)-[~/Desktop/PEN200/Feast/MS01]
└─$ nxc smb nmap/ip.txt  -u users -p 'BigFeast999!' | grep '[+]'
SMB                      192.168.245.169 445    DC01             [+] feast.com\administrator:BigFeast999! (Pwn3d!)
SMB                      192.168.245.170 445    MS01             [+] feast.com\administrator:BigFeast999! (Pwn3d!)
SMB                      192.168.245.171 445    MS02             [+] feast.com\administrator:BigFeast999! (Pwn3d!)


# Steps to DC01

### Root flag

Administrator:BigFeast999! validates to all services on DC01. 

Login via evilwinrm. Flag on Desktop


### Pivoting



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






