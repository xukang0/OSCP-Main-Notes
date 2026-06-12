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
22/tcp open  ssh     OpenSSH 8.2p1 Ubuntu 4ubuntu0.5 (Ubuntu Linux; protocol 2.0)
| ssh-hostkey: 
|   3072 62:36:1a:5c:d3:e3:7b:e1:70:f8:a3:b3:1c:4c:24:38 (RSA)
|   256 ee:25:fc:23:66:05:c0:c1:ec:47:c6:bb:00:c7:4f:53 (ECDSA)
|_  256 83:5c:51:ac:32:e5:3a:21:7c:f6:c2:cd:93:68:58:d8 (ED25519)

80/tcp open  http    Apache httpd 2.4.41 ((Ubuntu))
|_http-title: marketing.pg - Digital Marketing for you!
|_http-server-header: Apache/2.4.41 (Ubuntu)
Device type: general purpose|router
Running: Linux 5.X, MikroTik RouterOS 7.X
```

---
## Software Versions

```powershell
LimeSurvey Version 5.3.24 
```

---
## Discovered Subdomains

---
## Discovered Credentials

admin@marketing.pg


```
limesurvey_user
```
```
EzPwz2022_dev1$$23!!
```

```
$2y$10$QxdVgZGY9odLkWsUYF7dNOkI.STdeEWnUiUse/9rkI.lg7T3QI5UG
```

---
## Interesting Files/Paths

/var/www/LimeSurvey/application/extensions/bootstrap/tests/_data/dump.sql

---
## Attack Ideas

---
## Steps to User.txt

/old find http://customers-survey.marketing.pg subdomain

fuzzing this finds /admin

admin:password logins and finds LimeSurvey Community Ediiton V 5.3.24

https://github.com/Y1LD1R1M-1337/Limesurvey-RCE/blob/main/Y1LD1R1M.zip

Modify and rebuild the zip file

python exploit.py http://customers-survey.marketing.pg/ admin password 80

www-data shell obtained (no perms)

MySQL running on internal

Googled and found out LimeSurvey sql config file is called config-sample-mysql.php

find / -iname config-sample-mysql.php -type f 2>/dev/null 

Creds : limesurvey_user:

```
EzPwz2022_dev1$$23!!
```

This passwords allow su to t.miller for local.txt

---
## Steps to root.txt

---
## User Flag

```

```

## Root Flag

```

```