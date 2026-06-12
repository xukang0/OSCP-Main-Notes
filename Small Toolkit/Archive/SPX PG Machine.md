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
PORT   STATE SERVICE VERSION
22/tcp open  ssh     OpenSSH 8.9p1 Ubuntu 3ubuntu0.10 (Ubuntu Linux; protocol 2.0)
| ssh-hostkey: 
|   256 b9:bc:8f:01:3f:85:5d:f9:5c:d9:fb:b6:15:a0:1e:74 (ECDSA)
|_  256 53:d9:7f:3d:22:8a:fd:57:98:fe:6b:1a:4c:ac:79:67 (ED25519)


80/tcp open  http    Apache httpd 2.4.52 ((Ubuntu))
|_http-server-header: Apache/2.4.52 (Ubuntu)
|_http-title: Tiny File Manager
Warning: OSScan results may be unreliable because we could not find at least 1 open and 1 closed port
Device type: general purpose|router
Running (JUST GUESSING): Linux 4.X|5.X|3.X|6.X|2.6.X (97%), MikroTik RouterOS 7.X (94%)
OS CPE: cpe:/o:linux:linux_kernel:4 cpe:/o:linux:linux_kernel:5 cpe:/o:mikrotik:routeros:7 cpe:/o:linux:linux_kernel:5.6.3 cpe:/o:linux:linux_kernel:3 cpe:/o:linux:linux_kernel:6 cpe:/o:linux:linux_kernel:2.6
Aggressive OS guesses: Linux 4.15 - 5.19 (97%), Linux 5.0 - 5.14 (97%), MikroTik RouterOS 7.2 - 7.5 (Linux 5.6.3) (94%), Linux 3.10 - 4.11 (91%), Linux 3.2 - 4.14 (91%), Linux 5.14 - 6.8 (91%), Linux 2.6.32 - 3.10 (91%), Linux 2.6.32 - 3.13 (90%), Linux 3.4 - 3.10 (90%), OpenWrt 22.03 (Linux 5.10) (89%)
No exact OS matches for host (test conditions non-ideal).
Network Distance: 4 hops
Service Info: OS: Linux; CPE: cpe:/o:linux:linux_kernel
```

---
## Software Versions

```powershell

```

---
## Discovered Subdomains

---
## Discovered Credentials

profiler:x:1000:1000::/home/profiler:/bin/bash

---
## Interesting Files/Paths

Root dir : /var/www/html 

SPX_KEY : 	

```
a2a90ca2f9f0ea04d267b16fb8e63800
```

```
   'admin' => '$2y$10$7LaMUa8an8NrvnQsj5xZ3eDdOejgLyXE8IIvsC.hFy1dg7rPb9cqG',
    'user' => '$2y$10$x8PS6i0Sji2Pglyz7SLFruYFpAsz9XAYsdiPyfse6QDkB/QsdShxi'
```

---
## Attack Ideas

---
## Steps to User.txt

pfpinfo.php shows SPX_key

[[SPX PG Machine]] to file read index.php which contains admin hash

cracking admin hash allows tiny file manager acess

Upload reverse shell to tiny file manager for www-data shell

profiler:lowprofile allows user access

---
## Steps to root.txt

sudo -l reveals 

(ALL) /usr/bin/make install -C /home/profiler/php-spx

change SHELL attribtue in Makefile in /php-spx to bash /tmp/sh

nano sh "sudo -i"

then sudo /usr/bin/make install -C /home/profiler/php-spx grants me root

---
## User Flag

```

```

## Root Flag

```

```