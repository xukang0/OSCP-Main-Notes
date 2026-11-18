
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

---

# Steps to MS02 

### User flag




### Root flag



### Pivoting


# Steps to DC01

### User flag



### Root flag



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






