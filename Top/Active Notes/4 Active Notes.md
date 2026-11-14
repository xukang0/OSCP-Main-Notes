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
# Nmap 7.991 scan initiated Fri Nov 13 23:33:10 2026 as: /usr/lib/nmap/nmap -vvv -p 22 -4 -sC -sV -Pn --append-output -oN all_hosts1.txt 192.168.162.122
Nmap scan report for 192.168.162.122
PORT   STATE    SERVICE REASON      VERSION
22/tcp filtered ssh     no-response

Nmap scan report for 192.168.162.120
PORT   STATE    SERVICE REASON      VERSION
22/tcp filtered ssh     no-response
80/tcp filtered http    no-response

Nmap scan report for WEB02.dmz.medtech.com (192.168.162.121)
PORT    STATE    SERVICE     REASON      VERSION
80/tcp  filtered http        no-response
135/tcp filtered msrpc       no-response
139/tcp filtered netbios-ssn no-response

Nmap scan report for 172.16.162.11
PORT      STATE SERVICE REASON         VERSION
49664/tcp open  msrpc   syn-ack ttl 64 Microsoft Windows RPC
49665/tcp open  msrpc   syn-ack ttl 64 Microsoft Windows RPC
49666/tcp open  msrpc   syn-ack ttl 64 Microsoft Windows RPC
49667/tcp open  msrpc   syn-ack ttl 64 Microsoft Windows RPC
49668/tcp open  msrpc   syn-ack ttl 64 Microsoft Windows RPC
49669/tcp open  msrpc   syn-ack ttl 64 Microsoft Windows RPC
49674/tcp open  msrpc   syn-ack ttl 64 Microsoft Windows RPC
Service Info: OS: Windows; CPE: cpe:/o:microsoft:windows

Nmap scan report for 172.16.162.10
PORT      STATE SERVICE    REASON         VERSION
49664/tcp open  msrpc      syn-ack ttl 64 Microsoft Windows RPC
49665/tcp open  msrpc      syn-ack ttl 64 Microsoft Windows RPC
49666/tcp open  msrpc      syn-ack ttl 64 Microsoft Windows RPC
49667/tcp open  msrpc      syn-ack ttl 64 Microsoft Windows RPC
49668/tcp open  msrpc      syn-ack ttl 64 Microsoft Windows RPC
49672/tcp open  msrpc      syn-ack ttl 64 Microsoft Windows RPC
58963/tcp open  ncacn_http syn-ack ttl 64 Microsoft Windows RPC over HTTP 1.0
65357/tcp open  msrpc      syn-ack ttl 64 Microsoft Windows RPC
Service Info: OS: Windows; CPE: cpe:/o:microsoft:windows

Nmap scan report for 172.16.162.82
PORT      STATE SERVICE REASON         VERSION
5040/tcp  open  unknown syn-ack ttl 64
49664/tcp open  msrpc   syn-ack ttl 64 Microsoft Windows RPC
49665/tcp open  msrpc   syn-ack ttl 64 Microsoft Windows RPC
49666/tcp open  msrpc   syn-ack ttl 64 Microsoft Windows RPC
49667/tcp open  msrpc   syn-ack ttl 64 Microsoft Windows RPC
49668/tcp open  msrpc   syn-ack ttl 64 Microsoft Windows RPC
49669/tcp open  msrpc   syn-ack ttl 64 Microsoft Windows RPC
49670/tcp open  msrpc   syn-ack ttl 64 Microsoft Windows RPC
49671/tcp open  msrpc   syn-ack ttl 64 Microsoft Windows RPC

Nmap scan report for 172.16.162.13
PORT      STATE SERVICE REASON         VERSION
49664/tcp open  unknown syn-ack ttl 64
49665/tcp open  msrpc   syn-ack ttl 64 Microsoft Windows RPC
49666/tcp open  msrpc   syn-ack ttl 64 Microsoft Windows RPC
49667/tcp open  msrpc   syn-ack ttl 64 Microsoft Windows RPC
49668/tcp open  msrpc   syn-ack ttl 64 Microsoft Windows RPC
49669/tcp open  msrpc   syn-ack ttl 64 Microsoft Windows RPC
49674/tcp open  unknown syn-ack ttl 64

Nmap scan report for 172.16.162.12
PORT      STATE SERVICE REASON         VERSION
49664/tcp open  msrpc   syn-ack ttl 64 Microsoft Windows RPC
49665/tcp open  msrpc   syn-ack ttl 64 Microsoft Windows RPC
49666/tcp open  msrpc   syn-ack ttl 64 Microsoft Windows RPC
49667/tcp open  msrpc   syn-ack ttl 64 Microsoft Windows RPC
49668/tcp open  msrpc   syn-ack ttl 64 Microsoft Windows RPC
49669/tcp open  msrpc   syn-ack ttl 64 Microsoft Windows RPC
49670/tcp open  msrpc   syn-ack ttl 64 Microsoft Windows RPC

Nmap scan report for WEB02.dmz.medtech.com (192.168.162.121)
PORT      STATE SERVICE     REASON          VERSION
5985/tcp  open  http        syn-ack ttl 125 Microsoft HTTPAPI httpd 2.0 (SSDP/UPnP)
|_http-server-header: Microsoft-HTTPAPI/2.0
|_http-title: Not Found
5986/tcp  open  ssl/wsmans? syn-ack ttl 125
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

Nmap scan report for 172.16.162.83
PORT      STATE SERVICE REASON         VERSION
5040/tcp  open  unknown syn-ack ttl 64
49664/tcp open  msrpc   syn-ack ttl 64 Microsoft Windows RPC
49665/tcp open  msrpc   syn-ack ttl 64 Microsoft Windows RPC
49666/tcp open  msrpc   syn-ack ttl 64 Microsoft Windows RPC
49667/tcp open  msrpc   syn-ack ttl 64 Microsoft Windows RPC
49668/tcp open  msrpc   syn-ack ttl 64 Microsoft Windows RPC
49669/tcp open  msrpc   syn-ack ttl 64 Microsoft Windows RPC
49673/tcp open  msrpc   syn-ack ttl 64 Microsoft Windows RPC

Nmap scan report for 192.168.162.122
PORT     STATE SERVICE  REASON         VERSION
1194/tcp open  openvpn? syn-ack ttl 61



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