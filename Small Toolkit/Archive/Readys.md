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
PORT     STATE SERVICE VERSION
22/tcp   open  ssh     OpenSSH 7.9p1 Debian 10+deb10u2 (protocol 2.0)
| ssh-hostkey: 
|   2048 74:ba:20:23:89:92:62:02:9f:e7:3d:3b:83:d4:d9:6c (RSA)
|   256 54:8f:79:55:5a:b0:3a:69:5a:d5:72:39:64:fd:07:4e (ECDSA)
|_  256 7f:5d:10:27:62:ba:75:e9:bc:c8:4f:e2:72:87:d4:e2 (ED25519)
80/tcp   open  http    Apache httpd 2.4.38 ((Debian))
|_http-title: Readys &#8211; Just another WordPress site
|_http-server-header: Apache/2.4.38 (Debian)
|_http-generator: WordPress 5.7.2
6379/tcp open  redis   Redis key-value store
Aggressive OS guesses: Linux 5.0 - 5.14 (98%), MikroTik RouterOS 7.2 - 7.5 (Linux 5.6.3) (98%), Linux 4.15 - 5.19 (94%), Linux 2.6.32 - 3.13 (93%), Linux 5.14 - 6.8 (93%), OpenWrt 22.03 (Linux 5.10) (93%), Linux 3.10 - 4.11 (91%), Linux 5.0 (91%), Linux 6.18 (91%), Linux 3.2 - 4.14 (90%)
No exact OS matches for host (test conditions non-ideal).
Network Distance: 4 hops
Service Info: OS: Linux; CPE: cpe:/o:linux:linux_kernel
```

---
## Software Versions

```powershell
WordPress version 5.7.2
redis_version:5.0.14
mysql  Ver 15.1 Distrib 10.3.31-MariaDB
```

---
## Discovered Subdomains

---
## Discovered Credentials

Alice

```
Ready4Redis?
```

╔══════════╣ Analyzing Wordpress Files (limit 70)
-rw-r--r-- 1 alice alice 3194 Nov 16  2021 /var/www/html/wp-config.php                                                                                                                                                                      
define( 'DB_NAME', 'wordpress' );
define( 'DB_USER', 'karl' );
define( 'DB_PASSWORD', 'Wordpress1234' );
define( 'DB_HOST', 'localhost' );

```admin
$P$Ba5uoSB5xsqZ5GFIbBnOkXA0ahSJnb0
```

---
## Interesting Files/Paths

/usr/local/bin/backup.sh

/opt/backups

/var/backups

/opt

/etc/mysql/mariadb.conf.d/
/etc/mysql/conf.d/
/etc/mysql/mariadb.cnf 

/etc/mysql/my.cnf
/etc/mysql/mariadb.conf.d/50-server.cnf

---
## Attack Ideas

Redis login after getting creds

---
## Steps to User.txt

Wordpress site, wordpress scan reveals site-editor LFI. 

Redis conf is on /etc/redis/redis.conf so use LFI to read password

Use password to auth into redis

Redis version 5.0.1.

Use [[6379 Redis]] method to gain alice shell

---
## Steps to root.txt

backup.sh cronjob shows tar wildcard file

[[Wildcard Hijack]] and add +s to /bin/bash

/bin/bash -p for root

---
## User Flag

```

```

## Root Flag

```

```