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
135/tcp   open  msrpc           syn-ack ttl 125 Microsoft Windows RPC
139/tcp   open  netbios-ssn     syn-ack ttl 125 Microsoft Windows netbios-ssn
445/tcp   open  microsoft-ds?   syn-ack ttl 125
5001/tcp  open  commplex-link?  syn-ack ttl 125
| fingerprint-strings: 
|   SIPOptions: 
|     HTTP/1.1 200 OK
|     Content-Type: text/html; charset=ISO-8859-1
|     Content-Length: 132
|_    MAINSERVER_RESPONSE:<serverinfo method="setserverinfo" mainserver="5001" webserver="44444" pxyname="192.168.45.178" startpage=""/>
5040/tcp  open  unknown         syn-ack ttl 125
5985/tcp  open  http            syn-ack ttl 125 Microsoft HTTPAPI httpd 2.0 
5986/tcp  open  ssl/wsmans?     syn-ack ttl 125
7680/tcp  open  pando-pub?      syn-ack ttl 125
12000/tcp open  cce4x?          syn-ack ttl 125
44444/tcp open  cognex-dataman? syn-ack ttl 125
47001/tcp open  http            syn-ack ttl 125 Microsoft HTTPAPI httpd 2.0 (SSDP/UPnP)
|_http-title: Not Found
|_http-server-header: Microsoft-HTTPAPI/2.0
49664/tcp open  msrpc           syn-ack ttl 125 Microsoft Windows RPC
49665/tcp open  msrpc           syn-ack ttl 125 Microsoft Windows RPC
49666/tcp open  msrpc           syn-ack ttl 125 Microsoft Windows RPC
49667/tcp open  msrpc           syn-ack ttl 125 Microsoft Windows RPC
49668/tcp open  msrpc           syn-ack ttl 125 Microsoft Windows RPC
49669/tcp open  msrpc           syn-ack ttl 125 Microsoft Windows RPC
49670/tcp open  msrpc           syn-ack ttl 125 Microsoft Windows RPC
49671/tcp open  msrpc           syn-ack ttl 125 Microsoft Windows RPC
49672/tcp open  msrpc           syn-ack ttl 125 Microsoft Windows RPC
49676/tcp open  tcpwrapped      syn-ack ttl 125
52187/tcp open  java-rmi        syn-ack ttl 125 Java RMI
52218/tcp open  unknown         syn-ack ttl 125
57744/tcp open  unknown         syn-ack ttl 125
57745/tcp open  unknown         syn-ack ttl 125
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