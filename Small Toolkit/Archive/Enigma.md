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
111/udp   open          rpcbind

PORT      STATE SERVICE  VERSION
22/tcp    open  ssh      OpenSSH 9.6p1 Ubuntu 3ubuntu13.16 (Ubuntu Linux; protocol 
80/tcp    open  http     nginx 1.24.0 (Ubuntu)
|_http-title: Did not follow redirect to http://enigma.htb/
|_http-server-header: nginx/1.24.0 (Ubuntu)
110/tcp   open  pop3     Dovecot pop3d
| ssl-cert: Subject: commonName=enigma
| Subject Alternative Name: DNS:enigma
| rpcinfo: 
|   program version    port/proto  service
|   100000  2,3,4        111/tcp   rpcbind
|   100000  2,3,4        111/udp   rpcbind
|   100000  3,4          111/tcp6  rpcbind
|   100000  3,4          111/udp6  rpcbind
|   100003  3,4         2049/tcp   nfs
|   100003  3,4         2049/tcp6  nfs
|   100005  1,2,3      32899/tcp6  mountd
|   100005  1,2,3      32905/udp   mountd
|   100005  1,2,3      33810/udp6  mountd
|   100005  1,2,3      38909/tcp   mountd
|   100021  1,3,4      33731/udp6  nlockmgr
|   100021  1,3,4      35547/tcp   nlockmgr
|   100021  1,3,4      37943/tcp6  nlockmgr
|   100021  1,3,4      54671/udp   nlockmgr
|   100024  1          33257/tcp6  status
|   100024  1          37846/udp6  status
|   100024  1          48563/tcp   status
|   100024  1          52285/udp   status
|   100227  3           2049/tcp   nfs_acl
|_  100227  3           2049/tcp6  nfs_acl
143/tcp   open  imap     Dovecot imapd (Ubuntu)

993/tcp   open  ssl/imap Dovecot imapd (Ubuntu)

995/tcp   open  ssl/pop3 Dovecot pop3d

2049/tcp  open  nfs_acl  3 (RPC #100227)
32951/tcp open  mountd   1-3 (RPC #100005)
35547/tcp open  nlockmgr 1-4 (RPC #100021)
37715/tcp open  mountd   1-3 (RPC #100005)
38909/tcp open  mountd   1-3 (RPC #100005)
48563/tcp open  status   1 (RPC #100024)
Device type: general purpose
Running: Linux 4.X|5.X
OS CPE: cpe:/o:linux:linux_kernel:4 cpe:/o:linux:linux_kernel:5
OS details: Linux 4.15 - 5.19
Network Distance: 2 hops
Service Info: OS: Linux; CPE: cpe:/o:linux:linux_kernel

TRACEROUTE (using port 995/tcp)
HOP RTT      ADDRESS
1   96.15 ms 10.10.16.1
2   26.33 ms 10.129.7.227
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

Vhost fuzzing discovers mail001.enigma.htb [Roundcube webmail]

---
## Steps to root.txt

---
## User Flag

```

```

## Root Flag

```

```