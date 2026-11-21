[[Active Notes Template]]
## Provided Credentials
---

```

```

```

```

---
## Open Ports

```powershell
21/tcp   open  ftp     syn-ack ttl 61 vsftpd 3.0.3
22/tcp   open  ssh     syn-ack ttl 61 OpenSSH 7.2p2 Ubuntu 4ubuntu2.8 (Ubuntu 
80/tcp   open  http    syn-ack ttl 61 Apache httpd 2.4.18 ((Ubuntu))
3305/tcp open  http    syn-ack ttl 61 Apache httpd 2.4.18 ((Ubuntu))
8080/tcp open  http    syn-ack ttl 61 Apache httpd 2.4.18 ((Ubuntu))
```

---
## Software Versions

```powershell

```

---
## Discovered Subdomains

---
## Discovered Credentials

---
## Interesting Files/Paths

---
## Attack Ideas

---
## Steps to User.txt

Ping 192.168.132.52 shows tl=61 so this is a linux box

Nmap scan to show lists of ports
Let a slower rustscan run in the background

Port 21 : Anonymous FTP login failed

Port 80 : Pebbles login page

Port 3305 : Ubuntu default page

Page 8080 : Tomcat manager

Attempt to dirr bust against all web ports

We find /javascript/ (no access) and /zm/

/zm/ leads us to an interesting ZoneMinder Console - Running - default v1.29.0 dashboard

attemp to searchsploit for this 

There is a ZoneMinder Snapshots < 1.37.33 - Unauthenticated RCE.

use PythonDetector to find out it is python3

Upload perl RCE shell and get RCE as www-data

---
## Steps to root.txt

No Sudo -l, cap or SUID

LSE.sh tells us its vulnerable to PwnKit. Works and we are root. Flag at /root/proof.txt

---
## User Flag

```

```

## Root Flag

```

```