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
135/tcp   open  msrpc         syn-ack ttl 125 Microsoft Windows RPC
139/tcp   open  netbios-ssn   syn-ack ttl 125 Microsoft Windows netbios-ssn
445/tcp   open  microsoft-ds? syn-ack ttl 125
3306/tcp  open  mysql         syn-ack ttl 125 MariaDB 10.3.24 or later
5040/tcp  open  unknown       syn-ack ttl 125
5985/tcp  open  http          syn-ack ttl 125 Microsoft HTTPAPI httpd 2.0 
5986/tcp  open  ssl/wsmans?   syn-ack ttl 125
7680/tcp  open  pando-pub?    syn-ack ttl 125
47001/tcp open  http          syn-ack ttl 125 Microsoft HTTPAPI httpd 2.0
49664/tcp open  msrpc         syn-ack ttl 125 Microsoft Windows RPC
49665/tcp open  msrpc         syn-ack ttl 125 Microsoft Windows RPC
49666/tcp open  msrpc         syn-ack ttl 125 Microsoft Windows RPC
49667/tcp open  msrpc         syn-ack ttl 125 Microsoft Windows RPC
49668/tcp open  msrpc         syn-ack ttl 125 Microsoft Windows RPC
49669/tcp open  msrpc         syn-ack ttl 125 Microsoft Windows RPC
49670/tcp open  msrpc         syn-ack ttl 125 Microsoft Windows RPC
49671/tcp open  msrpc         syn-ack ttl 125 Microsoft Windows RPC
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


[[Current Affairs Notes Template]]

# Machine 1

# Steps to User flag

Sync time due to clock skew

domain name is secura.yzx

fdqn is dc01.secura.yzx

add secura.yzx to /etc/hosts

Ports
53 : dig nothing
135 : RPCclient nothing
139 :  nothing

With Eric.wallows creds and nxc weep, he has access to

SMB Shares
LDAP
RPC

Charlotte creds show win-rm pwned

Flag on her desktop

whoami/priv shows SeImpersonatePrivilege. Priv esc using PrintSpoofer

Get shell as secura\dc01

# Machine 2

# Steps to User flag

Sync time due to clock skew

fqdn is era.secura.yzx
NetBIOS computer name: ERA
NetBIOS domain name: SECURA
DNS domain: secura.yzx
FQDN: era.secura.yzx

With Eric.wallows creds and nxc weep, he has access to

RPC

After entering through Evil-WinRM as era/apache,

netstat ano shows 3306 running, locate mysql.exe

.\mysql.exe -u root -h 127.0.0.1 -e "use creds; select * from creds;"

administrator	Almost4There8.?
charlotte	Game2On4.!

Check creds with nxc. Only charlotte creds valid.

whoami /priv shows SeMachineAccountPrivilege and SeImpersonatePrivilege

# Machine 3

NetBIOS computer name: SECURE
NetBIOS domain name: SECURA
DNS domain: secura.yzx
FQDN: secure.secura.yzx
Derived membership: domain member
Derived domain: SECURA

Sus ports
5001
12000
44444
47001

Add secure.secura.yzx to /etc/hosts

"ManageEngine" webpage found at
http://secure.secura.yzx:44444/index.do

ManageEngine Build No:14710 listed

Google search shows CVE-2020-14008 for An authenticated administrator user can upload a malicious or vulnerable `.jar` file to a specific location via the network, resulting in **Remote Code Execution (RCE)**.

also, **CVE-2020-15394:** Unauthenticated SQL Injection via the REST API in Applications Manager _before_ build 14740 (Critical, CVSS 9.8), leading to remote code execution. [[1](https://nvd.nist.gov/vuln/detail/CVE-2020-15394)] NOT USING

Searching for ManageEngine Build No:14710 creds shows admin:admin. It works and we enter admin dashboard

Based on poc, generate weblogic.jar using msfvenom and Upload the JAR to `classes/weblogic/version8/` 

---

Creds are given Eric.Wallows : EricLikesRunning800

Run nxc credential sweep, it shows 

WinRM, RDP, RPC, WMI, SMB are pwned

On Eric winrm, eric is local administrator.

Using mimikatz, I found creds era@secura.local:New2Era4.!

also  * Username : SECURE$
	 * Domain   : SECURA
	 * NTLM     : 983e73c648db56f78e9dfb9698066734

Using Seatbelt.exe, RDCMan.settings shows 

        <userName>apache</userName>
        <password>New2Era4.!</password>

Login to era.secura.yzx

<profileName scope="Local">SECURE\apache</profileName>
<userName>apache</userName>
<domain>SECURE</domain>

evil-winrm -i 192.168.162.96 -u era.secura.yzx\\apache 

works




