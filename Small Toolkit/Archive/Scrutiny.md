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
22/tcp  open  ssh      syn-ack ttl 63 OpenSSH 9.6p1 Ubuntu 3ubuntu13.18 (Ubuntu Linux; protocol 2.0)
| ssh-hostkey: 
|   256 0c:4b:d2:76:ab:10:06:92:05:dc:f7:55:94:7f:18:df (ECDSA)
| ecdsa-sha2-nistp256 AAAAE2VjZHNhLXNoYTItbmlzdHAyNTYAAAAIbmlzdHAyNTYAAABBBN9Ju3bTZsFozwXY1B2KIlEY4BA+RcNM57w4C5EjOw1QegUUyCJoO4TVOKfzy/9kd3WrPEj/FYKT2agja9/PM44=
|   256 2d:6d:4a:4c:ee:2e:11:b6:c8:90:e6:83:e9:df:38:b0 (ED25519)
|_ssh-ed25519 AAAAC3NzaC1lZDI1NTE5AAAAIH9qI0OvMyp03dAGXR0UPdxw7hjSwMR773Yb9Sne+7vD
80/tcp  open  http     syn-ack ttl 63 nginx 1.24.0 (Ubuntu)
| http-methods: 
|_  Supported Methods: GET HEAD POST OPTIONS
|_http-server-header: nginx/1.24.0 (Ubuntu)
|_http-title: Did not follow redirect to https://cohort.htb/
443/tcp open  ssl/http syn-ack ttl 63 nginx 1.24.0 (Ubuntu)
|_ssl-date: TLS randomness does not represent time
|_http-server-header: nginx/1.24.0 (Ubuntu)
| http-methods: 
|_  Supported Methods: GET HEAD POST OPTIONS
| ssl-cert: Subject: commonName=cohort.htb/organizationName=Cohort Analytics
| Subject Alternative Name: DNS:cohort.htb, DNS:*.cohort.htb
| Issuer: commonName=cohort.htb/organizationName=Cohort Analytics
| Public Key type: rsa
| Public Key bits: 2048
| Signature Algorithm: sha256WithRSAEncryption
| Not valid before: 2026-06-01T18:47:07
| Not valid after:  2126-05-08T18:47:07
| MD5:     2e50 cc1d 45e6 73fd 12c5 9e21 82f2 c0ae
| SHA-1:   7e85 23e7 63eb 6541 a236 a388 fdc5 2514 8ca9 8e8c
| SHA-256: b5a8 18c7 eb3c 1923 8381 2665 afcb 2e69 85e7 b6f4 84e2 5378 205d b746 e58c b39f

```

---
## Software Versions

```powershell

```

---
## Discovered Subdomains

---
## Discovered Credentials

marcot:cheer
matthewa:IdealismEngineAshen476
Dach:RefriedScabbedWasting502

---
## Interesting Files/Paths

---
## Attack Ideas

---
## Steps to User.txt

Top right menu icon opens a login page button

Login page button shows hostname teams.onlyrands.com, add to /etc/hosts

This login page shows TeamCity Professional 2023.05.4

Searchsploit gives authentication bypass POC

This POC creates admin user ibrahimsql:ibrahimsql

https://github.com/hotplugin0x01/CVE-2023-42793

TeamCity HTB runner box

requesting admin token to disable debug mode

---
## Steps to root.txt

---
## User Flag

```

```

## Root Flag

```

```