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
21/tcp   open  ftp     syn-ack ttl 61 vsftpd 3.0.3
22/tcp   open  ssh     syn-ack ttl 61 OpenSSH 7.2p2 Ubuntu 4ubuntu2.8 (Ubuntu 
80/tcp   open  http    syn-ack ttl 61 Apache httpd 2.4.18 ((Ubuntu))
3305/tcp open  http    syn-ack ttl 61 Apache httpd 2.4.18 ((Ubuntu))
8080/tcp open  http    syn-ack ttl 61 Apache httpd 2.4.18 ((Ubuntu))
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

---
## Steps to User.txt

Ping 192.168.132.52 shows tl=61 so this is a linux box

Nmap scan to show lists of ports
Let a slower rustscan run in the background

Port 21 : Anonymous FTP login failed

Port 80 : Pebbles login page

Port 3305 : Ubuntu default page

Page 8080 : Tomcat manager



---
## Steps to root.txt

---
## User Flag

```

```

## Root Flag

```

```