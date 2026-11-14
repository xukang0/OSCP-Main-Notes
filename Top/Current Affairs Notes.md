
[[Current Affairs Notes Template]]

---
# Steps to WEB02 

### Initial access

Nmap scans shows

Machine 3 : SSH, 80
Machine 4: 80, 135, 139, 47001
Machine 5 : SSH 

Looks like the foucs is machine 4. Visit webpage 80. Medtech website. Uses .ASPX. Dir Fuzz.
There is a patient login portal at login.aspx

From enum4linux ng we get some domain information

[+] Found domain information via SMB
NetBIOS computer name: WEB02
NetBIOS domain name: MEDTECH
DNS domain: medtech.com
FQDN: WEB02.dmz.medtech.com
Derived membership: domain member
Derived domain: MEDTECH

Test' on medtech patient portal shows mssql error.

Get RCE to land on nt service\mssql$sqlexpress

### Root flag

SeImpersonatePriv exists [[SharpEfsPotato]]

Flag on Administrator desktop


---

# Steps to MS02 

### User flag

in joe downloads on WEB02 root, there is test.zip 

Inside contains web.config with creds to user SA.

Realize WEB02 root has access to internel subnet. Ligolo pivot to internal subnet. Nmap scan.


### Root flag



# Steps to DC01

### User flag



### Root flag




---

# Steps to Frankfurt
### User flag



### Root flag

---
# Steps to Charlie
### User flag



### Root flag



---
# Steps to Pascha
### User flag



### Root flag






