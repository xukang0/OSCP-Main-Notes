[[Active Notes Template]]
## Provided Credentials
---

```

```

```

```

---
## Open Ports

| Port | Service | Notes |
| ---- | ------- | ----- |
|      |         |       |

```powershell
22/tcp   open  ssh     OpenSSH 8.9p1 Ubuntu 3ubuntu0.10 (Ubuntu Linux; protocol 2.0)
| ssh-hostkey: 
|   256 2e:5b:cb:6b:21:8c:fc:df:7b:c7:f7:f0:46:2e:6d:55 (ECDSA)
|_  256 ab:1a:ce:a7:f0:b6:0f:79:0b:54:b8:00:26:3d:69:58 (ED25519)

80/tcp   open  http    Apache httpd 2.4.52 ((Ubuntu))
|_http-title: Apache2 Ubuntu Default Page: It works
|_http-server-header: Apache/2.4.52 (Ubuntu)

6789/tcp open  http    Tornado httpd 6.3.3
|_http-server-header: TornadoServer/6.3.3
|_http-title: Mage

```


---
## Software Versions

```powershell
Mage v0.9.75

TornadoServer/6.3.3
```


---
## Discovered Subdomains




---
## Discovered Credentials

root:x:0:0:root:/root:/bin/bash
ubuntu:x:1000:1001:Ubuntu:/home/ubuntu:/bin/bash

| Username | Password | Notes |
| -------- | -------- | ----- |
|          |          |       |
$DB['TYPE']                     = 'MYSQL';
$DB['SERVER']                   = 'localhost';
$DB['PORT']                     = '0';
$DB['DATABASE']                 = 'zabbix';
$DB['USER']                     = 'zabbix';
$DB['PASSWORD']                 = 'breadandbuttereater121';


---
## Attack Angles

/var/www/.mage_data/html/mage-aidb.db

/usr/bin/python3 /usr/local/bin/mage start

/usr/bin/python3 -m ipykernel_launcher -f /tmp/tmpi6m_t17u.json





---
## Steps to User.txt

port 9443 shows terminal which grants me www-data. Local.txt

---
## Steps to root.txt

ss -tlpn to find 10050 zabbix ports

Chisel port 80 /zabbix to my lcoalhost

Find mysql creds, login to mysql and find admin and hash

John the ripper to crack hash

login admin dashboard

create script, run reverse shell. Enter as user zabbix

sudo -l for /usr/bin/rsync

gtfobins and root easily

---

## User Flag

```

```

## Root Flag

```

```