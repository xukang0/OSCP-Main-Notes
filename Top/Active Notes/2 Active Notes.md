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
Open 192.168.245.143:22
Open 192.168.245.143:21
Open 192.168.245.143:80
Open 192.168.245.143:81
Open 192.168.245.143:443
Open 192.168.245.143:3000
Open 192.168.245.143:3001
Open 192.168.245.143:3003
Open 192.168.245.143:3306
Open 192.168.245.143:5432

PORT     STATE SERVICE    REASON         VERSION
21/tcp   open  ftp        syn-ack ttl 61 vsftpd 3.0.3
22/tcp   open  ssh        syn-ack ttl 61 OpenSSH 8.2p1 Ubuntu 4ubuntu0.4 (Ubuntu 
80/tcp   open  http       syn-ack ttl 61 Apache httpd 2.4.41 ((Ubuntu))
81/tcp   open  http       syn-ack ttl 61 Apache httpd 2.4.41 ((Ubuntu))
443/tcp  open  http       syn-ack ttl 61 Apache httpd 2.4.41
3000/tcp open  ppp?       syn-ack ttl 61
3001/tcp open  nessus?    syn-ack ttl 61
3003/tcp open  cgms?      syn-ack ttl 61
3306/tcp open  mysql      syn-ack ttl 61 MySQL (unauthorized)
5432/tcp open  postgresql syn-ack ttl 61 PostgreSQL DB 12.9 - 12.13

```

---
## Software Versions

```powershell

```

---
## Discovered Subdomains

---
## Discovered Credentials

---
## Interesting Files/Paths

---
## Attack Ideas

Dirbust port 80 + 81 + 443

---
## Steps to User.txt

Port 80 + 443 is apache default page

Port 81 is nginx fedora default page

---
## Steps to root.txt

---
## User Flag

```

```

## Root Flag

```

```