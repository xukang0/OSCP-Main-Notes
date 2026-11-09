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
21/tcp    open  ftp            syn-ack ttl 125 Microsoft ftpd
| ftp-syst: 
|_  SYST: Windows_NT
22/tcp    open  ssh            syn-ack ttl 125 OpenSSH for_Windows_8.1 (protocol 2.0)
135/tcp   open  msrpc          syn-ack ttl 125 Microsoft Windows RPC
139/tcp   open  netbios-ssn    syn-ack ttl 125 Microsoft Windows netbios-ssn
445/tcp   open  microsoft-ds?  syn-ack ttl 125
5040/tcp  open  unknown        syn-ack ttl 125
5985/tcp  open  http           syn-ack ttl 125 Microsoft HTTPAPI httpd 2.0 
5986/tcp  open  ssl/wsmans?    syn-ack ttl 125
7680/tcp  open  pando-pub?     syn-ack ttl 125
8000/tcp  open  http           syn-ack ttl 125 Microsoft IIS httpd 10.0
8080/tcp  open  http           syn-ack ttl 125 Microsoft HTTPAPI httpd 2.0 
8443/tcp  open  ssl/https-alt? syn-ack ttl 125

| ssl-cert: Subject: commonName=MS01.oscp.exam
| Subject Alternative Name: DNS:MS01.oscp.exam
| Issuer: commonName=MS01.oscp.exam

47001/tcp open  http           syn-ack ttl 125 Microsoft HTTPAPI httpd 2.0 (SSDP/UPnP)
|_http-title: Not Found
|_http-server-header: Microsoft-HTTPAPI/2.0
49664/tcp open  msrpc          syn-ack ttl 125 Microsoft Windows RPC
49665/tcp open  msrpc          syn-ack ttl 125 Microsoft Windows RPC
49666/tcp open  msrpc          syn-ack ttl 125 Microsoft Windows RPC
49667/tcp open  msrpc          syn-ack ttl 125 Microsoft Windows RPC
49668/tcp open  msrpc          syn-ack ttl 125 Microsoft Windows RPC
49669/tcp open  msrpc          syn-ack ttl 125 Microsoft Windows RPC
49670/tcp open  msrpc          syn-ack ttl 125 Microsoft Windows RPC
49671/tcp open  msrpc          syn-ack ttl 125 Microsoft Windows RPC
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