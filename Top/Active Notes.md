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
# Nmap 7.99 scan initiated Sat Jun 13 23:24:39 2026 as: /usr/lib/nmap/nmap -A -Pn -T4 -p- --open -oA fulltcp_scan 192.168.127.91
Nmap scan report for 192.168.127.91
Host is up (0.0081s latency).
Not shown: 65531 filtered tcp ports (no-response), 1 closed tcp port (reset)
Some closed ports may be reported as filtered due to --defeat-rst-ratelimit
PORT   STATE SERVICE VERSION
22/tcp open  ssh     OpenSSH 8.2p1 Ubuntu 4ubuntu0.11 (Ubuntu Linux; protocol 2.0)
| ssh-hostkey: 
|   3072 62:36:1a:5c:d3:e3:7b:e1:70:f8:a3:b3:1c:4c:24:38 (RSA)
|   256 ee:25:fc:23:66:05:c0:c1:ec:47:c6:bb:00:c7:4f:53 (ECDSA)
|_  256 83:5c:51:ac:32:e5:3a:21:7c:f6:c2:cd:93:68:58:d8 (ED25519)
25/tcp open  smtp    Postfix smtpd
| ssl-cert: Subject: commonName=onlyrands.com
| Subject Alternative Name: DNS:onlyrands.com
| Not valid before: 2024-06-07T09:33:24
|_Not valid after:  2034-06-05T09:33:24
|_smtp-commands: onlyrands.com, PIPELINING, SIZE 10240000, VRFY, ETRN, STARTTLS, ENHANCEDSTATUSCODES, 8BITMIME, DSN, SMTPUTF8, CHUNKING
|_ssl-date: TLS randomness does not represent time
80/tcp open  http    nginx 1.18.0 (Ubuntu)
|_http-server-header: nginx/1.18.0 (Ubuntu)
|_http-title: OnlyRands
Aggressive OS guesses: Linux 5.0 - 5.14 (98%), MikroTik RouterOS 7.2 - 7.5 (Linux 5.6.3) (98%), Linux 4.15 - 5.19 (94%), Linux 2.6.32 - 3.13 (93%), Linux 5.14 - 6.8 (93%), OpenWrt 22.03 (Linux 5.10) (93%), Linux 5.0 (92%), Linux 3.10 - 4.11 (91%), Linux 6.18 (91%), Linux 3.2 - 4.14 (90%)
No exact OS matches for host (test conditions non-ideal).
Network Distance: 4 hops
Service Info: Host:  onlyrands.com; OS: Linux; CPE: cpe:/o:linux:linux_kernel

TRACEROUTE (using port 22/tcp)
HOP RTT     ADDRESS
1   7.53 ms 192.168.45.1
2   6.87 ms 192.168.45.254
3   8.22 ms 192.168.251.1
4   8.21 ms 192.168.127.91

OS and Service detection performed. Please report any incorrect results at https://nmap.org/submit/ .
# Nmap done at Sat Jun 13 23:26:37 2026 -- 1 IP address (1 host up) scanned in 118.24 seconds

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

---
## Steps to root.txt

---
## User Flag

```

```

## Root Flag

```

```