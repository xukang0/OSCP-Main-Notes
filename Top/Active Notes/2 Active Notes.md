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
PORT      STATE SERVICE     REASON         VERSION
22/tcp    open  ssh         syn-ack ttl 61 OpenSSH 7.9p1 Debian 10+deb10u2 

139/tcp   open  netbios-ssn syn-ack ttl 61 Samba smbd 3.X - 4.X (workgroup: WORKGROUP)

445/tcp   open  netbios-ssn syn-ack ttl 61 Samba smbd 4.9.5-Debian (workgroup: WORKGROUP)

631/tcp   open  ipp         syn-ack ttl 61 CUPS 2.2
| http-methods: 
|   Supported Methods: GET HEAD OPTIONS POST PUT
|_  Potentially risky methods: PUT
|_http-title: Forbidden - CUPS v2.2.10
|_http-server-header: CUPS/2.2 IPP/2.1

2181/tcp  open  zookeeper   syn-ack ttl 61 Zookeeper 3.4.6-1569965

2222/tcp  open  ssh         syn-ack ttl 61 OpenSSH 7.9p1 Debian 10+deb10u2 

8080/tcp  open  http        syn-ack ttl 61 Jetty 1.0
|_http-server-header: Jetty(1.0)
|_http-title: Error 404 Not Found

8081/tcp  open  http        syn-ack ttl 61 nginx 1.14.2
|_http-title: Did not follow redirect to http://192.168.213.98:8080/exhibitor/v1/ui/index.html
| http-methods: 
|_  Supported Methods: GET HEAD POST OPTIONS
|_http-server-header: nginx/1.14.2

39605/tcp open  java-rmi    syn-ack ttl 61 Java RMI
Service Info: Host: PELICAN; OS: Linux; CPE: cpe:/o:linux:linux_kernel

Host script results:
| smb-os-discovery: 
|   OS: Windows 6.1 (Samba 4.9.5-Debian)
|   Computer name: pelican
|   NetBIOS computer name: PELICAN\x00
|   Domain name: \x00
|   FQDN: pelican
|_  System time: 2026-11-22T16:26:56-05:00
| smb2-time: 
|   date: 2026-11-22T21:26:59
|_  start_date: N/A
| smb2-security-mode: 
|   3.1.1: 
|_    Message signing enabled but not required
| p2p-conficker: 
|   Checking for Conficker.C or higher...
|   Check 1 (port 63225/tcp): CLEAN (Couldn't establish connection (ERROR))
|   Check 2 (port 59002/tcp): CLEAN (Couldn't establish connection (ERROR))
|   Check 3 (port 37184/udp): CLEAN (Couldn't receive bytes: TIMEOUT)
|   Check 4 (port 54522/udp): CLEAN (Couldn't receive bytes: ERROR)
|_  0/4 checks are positive: Host is CLEAN or ports are blocked
| smb-security-mode: 
|   account_used: guest
|   authentication_level: user
|   challenge_response: supported
|_  message_signing: disabled (dangerous, but default)
|_clock-skew: mean: 1h39m59s, deviation: 2h53m12s, median: 0s
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

631 : Forbidden

2181 : Zookeeper 3.4.6-1569965

8080 : 404 not found

8081 : http://192.168.213.98:8080/exhibitor/v1/ui/index.html leads to Exhibitor for ZooKeeper
Page shows v1.0

39605/tcp open  java-rmi Running Java Remote Guesser shows not vulnerable (NOT CONFIRMED)

Dirr FUZZ (IMPT)

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