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
21/tcp   open  ftp     vsftpd 3.0.2
| ftp-syst: 
|   STAT: 
| FTP server status:
|      Connected to 192.168.45.232
|      Logged in as ftp
|      TYPE: ASCII
|      No session bandwidth limit
|      Session timeout in seconds is 300
|      Control connection is plain text
|      Data connections will be plain text
|      At session startup, client count was 4
|      vsFTPd 3.0.2 - secure, fast, stable
|_End of status
| ftp-anon: Anonymous FTP login allowed (FTP code 230)
|_drwxrwxrwx    2 0        0               6 Apr 01  2020 pub [NSE: writeable]


22/tcp   open  ssh     OpenSSH 7.4 (protocol 2.0)
| ssh-hostkey: 
|   2048 21:94:de:d3:69:64:a8:4d:a8:f0:b5:0a:ea:bd:02:ad (RSA)
|   256 67:42:45:19:8b:f5:f9:a5:a4:cf:fb:87:48:a2:66:d0 (ECDSA)
|_  256 f3:e2:29:a3:41:1e:76:1e:b1:b7:46:dc:0b:b9:91:77 (ED25519)


80/tcp   open  http    Apache httpd 2.4.6 ((CentOS) PHP/7.3.22)
|_http-generator: HTMLy v2.7.5
| http-cookie-flags: 
|   /: 
|     PHPSESSID: 
|_      httponly flag not set
| http-robots.txt: 11 disallowed entries 
| /config/ /system/ /themes/ /vendor/ /cache/ 
| /changelog.txt /composer.json /composer.lock /composer.phar /search/ 
|_/admin/
|_http-title: Sybaris - Just another HTMLy blog
|_http-server-header: Apache/2.4.6 (CentOS) PHP/7.3.22


6379/tcp open  redis   Redis key-value store 5.0.9

```


---
## Software Versions

```powershell

```


---
## Discovered Subdomains




---
## Discovered Credentials


| Username | Password | Notes |
| -------- | -------- | ----- |
|          |          |       |

---
## Attack Angles





---
## Steps to User.txt



---
## Steps to root.txt


---

## User Flag

```

```

## Root Flag

```

```