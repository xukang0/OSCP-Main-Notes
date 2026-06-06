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
22/tcp   open  ssh                    OpenSSH 8.2p1 Ubuntu 4ubuntu0.11 (Ubuntu Linux; protocol 2.0)
| ssh-hostkey: 
|   3072 51:56:a7:34:16:8e:3d:47:17:c8:96:d5:e6:94:46:46 (RSA)
|   256 fe:76:e3:4c:2b:f6:f5:21:a2:4d:9f:59:52:39:b9:16 (ECDSA)
|_  256 2c:dd:62:7d:d6:1c:f4:fd:a1:e4:c8:aa:11:ae:d6:1f (ED25519)

9090/tcp open  hadoop-tasktracker     Apache Hadoop
|_http-title: Site doesn't have a title (text/html).
| hadoop-datanode-info: 
|_  Logs: jive-ibtn jive-btn-gradient
| hadoop-tasktracker-info: 
|_  Logs: jive-ibtn jive-btn-gradient

9091/tcp open  ssl/hadoop-tasktracker Apache Hadoop
| hadoop-datanode-info: 
|_  Logs: jive-ibtn jive-btn-gradient
|_http-title: Site doesn't have a title (text/html).
| hadoop-tasktracker-info: 
|_  Logs: jive-ibtn jive-btn-gradient
|_ssl-date: TLS randomness does not represent time
| ssl-cert: Subject: commonName=localhost
| Subject Alternative Name: DNS:localhost, DNS:*.localhost
| Not valid before: 2024-06-28T07:02:39
|_Not valid after:  2029-06-27T07:02:39
```


---
## Software Versions

```powershell
Openfire, Version: 4.7.3
```


---
## Discovered Subdomains




---
## Discovered Credentials

('mail.smtp.username','root',0,NULL)
INSERT INTO OFPROPERTY VALUES('passwordKey','EOAJUe2Sqdlfqjk',0,NULL)

| Username | Password | Notes |
| -------- | -------- | ----- |
|          |          |       |

---
## Attack Angles





---
## Steps to User.txt

port 9090 shows openfire v 4.7.3

CVE-2023-32315, https://github.com/miko550/CVE-2023-32315 grants admin panel RCE.

Upload Reverse.sh to /tmp and receive Reverse shell

/openfire/local.txt

---
## Steps to root.txt

env shows /var/lib/openfire/embedded-db/ 

shows SMTP password, but no smtp port exists,

so su root:OpenFireAtEveryone grants root access

cat /root/proof.txt

---

## User Flag

```

```

## Root Flag

```

```