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
Nmap scan report for 192.168.162.121
Host is up, received user-set (0.049s latency).
Scanned at 2026-11-13 23:16:50 EST for 65s

PORT      STATE SERVICE     REASON          VERSION
80/tcp    open  http        syn-ack ttl 125 Microsoft IIS httpd 10.0
| http-methods: 
|   Supported Methods: OPTIONS TRACE GET HEAD POST
|_  Potentially risky methods: TRACE
|_http-title: MedTech
|_http-server-header: Microsoft-IIS/10.0
135/tcp   open  msrpc       syn-ack ttl 125 Microsoft Windows RPC
139/tcp   open  netbios-ssn syn-ack ttl 125 Microsoft Windows netbios-ssn
47001/tcp open  http        syn-ack ttl 125 Microsoft HTTPAPI httpd 2.0 (SSDP/UPnP)
|_http-server-header: Microsoft-HTTPAPI/2.0
|_http-title: Not Found
49664/tcp open  msrpc       syn-ack ttl 125 Microsoft Windows RPC
49665/tcp open  msrpc       syn-ack ttl 125 Microsoft Windows RPC
49666/tcp open  msrpc       syn-ack ttl 125 Microsoft Windows RPC
49667/tcp open  msrpc       syn-ack ttl 125 Microsoft Windows RPC
49668/tcp open  msrpc       syn-ack ttl 125 Microsoft Windows RPC
49671/tcp open  msrpc       syn-ack ttl 125 Microsoft Windows RPC
49677/tcp open  msrpc       syn-ack ttl 125 Microsoft Windows RPC
49689/tcp open  msrpc       syn-ack ttl 125 Microsoft Windows RPC
Service Info: OS: Windows; CPE: cpe:/o:microsoft:windows

```

---
## Software Versions

```powershell

```

---
## Discovered Subdomains

---
## Discovered Credentials

uid=sa;password=WhileChirpTuesday218

sa/WhileChirpTuesday218 and joe/Flowers1 doesnt seem to work anywhere

Secret  : _SC_SNMPTRAP / service 'SNMPTRAP' with username : MEDTECH\joe
cur/text: Flowers1

Secret  : _SC_SQLTELEMETRY$SQLEXPRESS / service 'SQLTELEMETRY$SQLEXPRESS' with username : NT Service\SQLTELEMETRY$SQLEXPRESS

Secret  : _SC_SSDPSRV / service 'SSDPSRV' with username : MEDTECH\joe
cur/text: Flowers1
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