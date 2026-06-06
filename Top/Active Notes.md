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
22/tcp open  ssh     OpenSSH 8.4p1 Debian 5+deb11u2 (protocol 2.0)
| ssh-hostkey: 
|   3072 c9:c3:da:15:28:3b:f1:f8:9a:36:df:4d:36:6b:a7:44 (RSA)
|   256 26:03:2b:f6:da:90:1d:1b:ec:8d:8f:8d:1e:7e:3d:6b (ECDSA)
|_  256 fb:43:b2:b0:19:2f:d3:f6:bc:aa:60:67:ab:c1:af:37 (ED25519)


80/tcp open  http    Apache httpd 2.4.56 ((Debian))
|_http-title: W3.CSS Template
|_http-server-header: Apache/2.4.56 (Debian)


```


---
## Software Versions

```powershell
Laravel 8.4.0
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

https://github.com/joshuavanderpoll/CVE-2021-3129?source=post_page-----12bfd272e9cf---------------------------------------

Found Laravel 8.4.0 at /password

Get RCE through CVE 2021 3129

Upload shell.sh through wget and execute to receive port 80 Reverse shell

Flag at /skunk/local.txt

---
## Steps to root.txt


---

## User Flag

```

```

## Root Flag

```

```