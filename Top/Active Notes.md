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
PORT      STATE SERVICE           VERSION
22/tcp    open  ssh               OpenSSH 7.4p1 Debian 10+deb9u7 (protocol 2.0)
|_auth-owners: root
| ssh-hostkey: 
|   2048 75:4c:02:01:fa:1e:9f:cc:e4:7b:52:fe:ba:36:85:a9 (RSA)
|   256 b7:6f:9c:2b:bf:fb:04:62:f4:18:c9:38:f4:3d:6b:2b (ECDSA)
|_  256 98:7f:b6:40:ce:bb:b5:57:d5:d1:3c:65:72:74:87:c3 (ED25519)


113/tcp   open  ident             FreeBSD identd
|_auth-owners: nobody


5432/tcp  open  postgresql        PostgreSQL DB
| fingerprint-strings: 
|   Kerberos: 
|     SFATAL
|     VFATAL
|     C0A000
|     Munsupported frontend protocol 27265.28208: server supports 

2.0 to 3.0
|     Fpostmaster.c
|     L2071
|     RProcessStartupPacket
|   SMBProgNeg: 
|     SFATAL
|     VFATAL
|     C0A000
|     Munsupported frontend protocol 65363.19778: server supports 

2.0 to 3.0
|     Fpostmaster.c
|     L2071
|_    RProcessStartupPacket

8080/tcp  open  http              WEBrick httpd 1.4.2 (Ruby 2.6.6 (2020-03-31))
| http-robots.txt: 4 disallowed entries 
|_/issues/gantt /issues/calendar /activity /search
|_http-title: Redmine
|_http-server-header: WEBrick/1.4.2 (Ruby/2.6.6/2020-03-31)

10000/tcp open  snet-sensor-mgmt?
|_auth-owners: eleanor
```


---
## Software Versions

```powershell

```


---
## Discovered Subdomains




---
## Discovered Credentials

```admin
TPG138735@#&a
```

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