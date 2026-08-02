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
135/tcp   open  msrpc         Microsoft Windows RPC
139/tcp   open  netbios-ssn   Microsoft Windows netbios-ssn
445/tcp   open  microsoft-ds?
3306/tcp  open  mysql         MariaDB 10.3.24 or later (unauthorized)
5040/tcp  open  unknown
7680/tcp  open  pando-pub?
8000/tcp  open  http-alt      BarracudaServer.com (Windows)
30021/tcp open  ftp           FileZilla ftpd 0.9.41 beta
|_ftp-bounce: bounce working!
| ftp-syst: 
|_  SYST: UNIX emulated by FileZilla
| ftp-anon: Anonymous FTP login allowed (FTP code 230)
| -r--r--r-- 1 ftp ftp            536 Nov 03  2020 .gitignore
| drwxr-xr-x 1 ftp ftp              0 Nov 03  2020 app
| drwxr-xr-x 1 ftp ftp              0 Nov 03  2020 bin
| drwxr-xr-x 1 ftp ftp              0 Nov 03  2020 config
| -r--r--r-- 1 ftp ftp            130 Nov 03  2020 config.ru
| drwxr-xr-x 1 ftp ftp              0 Nov 03  2020 db
| -r--r--r-- 1 ftp ftp           1750 Nov 03  2020 Gemfile
| drwxr-xr-x 1 ftp ftp              0 Nov 03  2020 lib
| drwxr-xr-x 1 ftp ftp              0 Nov 03  2020 log
| -r--r--r-- 1 ftp ftp             66 Nov 03  2020 package.json
| drwxr-xr-x 1 ftp ftp              0 Nov 03  2020 public
| -r--r--r-- 1 ftp ftp            227 Nov 03  2020 Rakefile
| -r--r--r-- 1 ftp ftp            374 Nov 03  2020 README.md
| drwxr-xr-x 1 ftp ftp              0 Nov 03  2020 test
| drwxr-xr-x 1 ftp ftp              0 Nov 03  2020 tmp
|_drwxr-xr-x 1 ftp ftp              0 Nov 03  2020 vendor
33033/tcp open  unknown
44330/tcp open  ssl/unknown
45332/tcp open  http          Apache httpd 2.4.46 ((Win64) OpenSSL/1.1.1g PHP/7.3.23)
|_http-server-header: Apache/2.4.46 (Win64) OpenSSL/1.1.1g PHP/7.3.23
|_http-title: Quiz App
| http-methods: 
|_  Potentially risky methods: TRACE
45443/tcp open  http          Apache httpd 2.4.46 ((Win64) OpenSSL/1.1.1g PHP/7.3.23)
|_http-title: Quiz App
| http-methods: 
|_  Potentially risky methods: TRACE
|_http-server-header: Apache/2.4.46 (Win64) OpenSSL/1.1.1g PHP/7.3.23
49664/tcp open  msrpc         Microsoft Windows RPC
49665/tcp open  msrpc         Microsoft Windows RPC
49666/tcp open  msrpc         Microsoft Windows RPC
49667/tcp open  msrpc         Microsoft Windows RPC
49668/tcp open  msrpc         Microsoft Windows RPC
49669/tcp open  msrpc         Microsoft Windows RPC

```

45332 Web quiz page
45443 Web quiz page
8000
5040

---
## Software Versions

```powershell
OS: Windows 10, Windows Server 2019, Windows Server 2016

BarracudaDrive 6.5

```

---
## Discovered Subdomains

---
## Discovered Credentials

---
## Interesting Files/Paths

secrets.yml from FTP
```powershell
# shared:
#   api_key: a1B2c3D4e5F6

# Environmental secrets are only available for that specific environment.

development:
  secret_key_base: 36c569c923cac0e10cddd6588b468d09e82eb8a3a25cee7274f1a6680fb0cb19f6c1a64cad5c57923aa4b89675315c9202a5ff8db67f84a150668d6949cc0846

test:
  secret_key_base: be9463a08fe11dd60d1ff4bd361392f994f5365445b6685b86ac65fa08d1a2c8772068af773f31b758475849117a231dc51ac60f3a937539ceff9dc3a3668c48

# Do not keep production secrets in the unencrypted secrets file.
# Instead, either read values from the environment.
# Or, use `bin/rails secrets:setup` to configure encrypted secrets
# and move the `production:` environment over there.

production:
  secret_key_base: <%= ENV["SECRET_KEY_BASE"] %>

```
---
## Attack Ideas

---
## Steps to User.txt

BarracudaDrive 5.6 discovered

Sign up for admin and access file manager

upload ivan sincek php webshell to C:\xampp\htdocs

Go to 192.168.107.127:45443/phpreverseshell.php

Get reverse shell as jerren

Flag on his desktop

---
## Steps to root.txt



---
## User Flag

```

```

## Root Flag

```

```