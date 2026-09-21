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
80/tcp    open  http         syn-ack ttl 127 Microsoft IIS httpd 10.0
| http-methods: 
|_http-title: Ask Jeeves
135/tcp   open  msrpc        syn-ack ttl 127 Microsoft Windows RPC
445/tcp   open  microsoft-ds syn-ack ttl 127 Microsoft Windows 7 - 10 microsoft-ds (workgroup: WORKGROUP)
50000/tcp open  http         syn-ack ttl 127 Jetty 9.4.z-SNAPSHOT
|_http-title: Error 404 Not Found
Service Info: Host: JEEVES; OS: Windows; CPE: cpe:/o:microsoft:windows



```

---
## Software Versions

```powershell
OS: Windows 10 Pro 10586
OS version: '10.0'
OS release: '1511'
OS build: '10586'
Native OS: Windows 10 Pro 10586
Native LAN manager: Windows 10 Pro 6.3

OS Name:                   Microsoft Windows 10 Pro
OS Version:                10.0.10586 N/A Build 10586
System Type:               x64-based PC

C:\Users\Administrator\.jenkins\secrets>wmic os get osarchitecture
wmic os get osarchitecture
OSArchitecture  
64-bit    

   TargetVersion    REG_SZ    4.0.0
    Version    REG_SZ    4.6.01038
    TargetVersion    REG_SZ    4.0.0
    Version    REG_SZ    4.6.01038
    TargetVersion    REG_SZ    4.0.0
    Version    REG_SZ    4.6.01038
    TargetVersion    REG_SZ    4.0.0
    Version    REG_SZ    4.6.01038
    Version    REG_SZ    4.0.0.0

```

---
## Discovered Subdomains

[+] Found domain information via SMB
NetBIOS computer name: JEEVES
NetBIOS domain name: ''
DNS domain: Jeeves
FQDN: Jeeves
Derived membership: workgroup member
Derived domain: unknown


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