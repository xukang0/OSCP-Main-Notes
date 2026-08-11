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
135/tcp   open  msrpc                Microsoft Windows RPC

RPCCLIENT TESTED

139/tcp   open  netbios-ssn          Microsoft Windows netbios-ssn


445/tcp   open  microsoft-ds?

ENUM4LINUX TESTED

3389/tcp  open  ms-wbt-server        Microsoft Terminal Services

3700/tcp  open  giop
| fingerprint-strings: 
|   GetRequest, X11Probe: 
|     GIOP
|   giop: 
|     GIOP
|     (IDL:omg.org/SendingContext/CodeBase:1.0
|     169.254.182.139
|     169.254.182.139
|_    default

?

4848/tcp  open  http                 Sun GlassFish Open Source Edition  4.1
|_http-title: Login
|_http-server-header: GlassFish Server Open Source Edition  4.1 
5040/tcp  open  unknown
6060/tcp  open  x11?

7676/tcp  open  java-message-service Java Message Service 301
	
7680/tcp  open  pando-pub?
8080/tcp  open  http                 Sun GlassFish Open Source Edition  4.1
|_http-title: Data Web
|_http-open-proxy: Proxy might be redirecting requests
| http-methods: 
|_  Potentially risky methods: PUT DELETE TRACE
|_http-server-header: GlassFish Server Open Source Edition  4.1 
8181/tcp  open  ssl/intermapper?

NOTHING

8686/tcp  open  java-rmi             Java RMI
| rmi-dumpregistry: 
|   jmxrmi
|     javax.management.remote.rmi.RMIServerImpl_Stub
|     @169.254.182.139:8686
|     extends
|       java.rmi.server.RemoteStub
|       extends
|_        java.rmi.server.RemoteObject
49664/tcp open  msrpc                Microsoft Windows RPC
49665/tcp open  msrpc                Microsoft Windows RPC
49666/tcp open  msrpc                Microsoft Windows RPC
49667/tcp open  msrpc                Microsoft Windows RPC
49668/tcp open  msrpc                Microsoft Windows RPC
49669/tcp open  msrpc                Microsoft Windows RPC
49670/tcp open  msrpc                Microsoft Windows RPC

```

---
## Software Versions

```powershell
OS: Windows 10, Windows Server 2019, Windows Server 2016
OS version: '10.0'
OS release: '2004'
OS build: '19041'

NetBIOS computer name: FISHYYY
NetBIOS domain name: ''
DNS domain: Fishyyy
FQDN: Fishyyy

SynaMan 5.1 build 1595
Synametrics File Manager.

Sun GlassFish Server Open Source Edition  4.1
```

Glassfish Path traversal for user entry. 

Then use SynaMan for priv esc.

---
## Discovered Subdomains

---
## Discovered Credentials

```
admin;{SSHA256}aLatQQ3qEJHinsX4N/+V/45mJwFSkXN5w7vz3P6kHy4jrX+U7hXCkQ==;asadmin
```

arthur
KingOfAtlantis

---
## Interesting Files/Paths

---
## Attack Ideas

---
## Steps to User.txt

Discover Oracle Glassfish 4.1 and directory traversal and file read CVE. 

Try to file read Synametric file manager 5.1.

SynaMan/config/AppConfig.xml

Find the creds arthur:KingOfAtlantis

RDP using these creds

local.txt on desktop

---
## Steps to root.txt



---
## User Flag

```

```

## Root Flag

```

```