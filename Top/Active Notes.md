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
21/tcp    open  ftp           FileZilla ftpd 0.9.41 beta
Lftp anonymous failed

80/tcp    open  http          Apache httpd 2.4.43 ((Win64) OpenSSL/1.1.1g PHP/7.4.6)
| http-title: Welcome to XAMPP
|_Requested resource was http://192.168.107.55/dashboard/
|_http-server-header: Apache/2.4.43 (Win64) OpenSSL/1.1.1g PHP/7.4.6

phpinfo found

135/tcp   open  msrpc         Microsoft Windows RPC
RPC tried

139/tcp   open  netbios-ssn   Microsoft Windows netbios-ssn
Tried

443/tcp   open  ssl/http      Apache httpd 2.4.43 ((Win64) OpenSSL/1.1.1g PHP/7.4.6)
Bad request
curling shows nothing

445/tcp   open  microsoft-ds?

Tried


3306/tcp  open  mysql         MariaDB 10.3.24 or later (unauthorized)
5040/tcp  open  unknown
Nothing

7680/tcp  open  pando-pub?
49664/tcp open  msrpc         Microsoft Windows RPC
49665/tcp open  msrpc         Microsoft Windows RPC
49666/tcp open  msrpc         Microsoft Windows RPC
49667/tcp open  msrpc         Microsoft Windows RPC
49668/tcp open  msrpc         Microsoft Windows RPC
49669/tcp open  msrpc         Microsoft Windows RPC

```

C:/xampp/htdocs 

---
## Software Versions

```powershell
XAMPP for Windows 7.4.6
Windows 10 x64

Apache 2.4.43
  + MariaDB 10.4.11
  + PHP 7.4.6 (VC15 X86 64bit thread safe) + PEAR
  + phpMyAdmin 5.0.2
  + OpenSSL 1.1.0g
  + ADOdb 518a
  + Mercury Mail Transport System v4.63 (not included in the portable version)
  + FileZilla FTP Server 0.9.41 (not included in the portable version)
  + Webalizer 2.23-04 (not included in the portable version)
  + Strawberry Perl 5.16.3.1 Portable
  + Tomcat 7.0.103
  + XAMPP Control Panel Version 3.2.4.
  + XAMPP mailToDisk 1.0 (write emails via PHP on local disk in <xampp>\mailoutput. Activated in the php.ini as mail default.)

```

---
## Discovered Subdomains

---
## Discovered Credentials

* PASSWORDS:

1) MySQL:

   User: root
   Password:
   (means no password!)

2) FileZilla FTP:

   [ You have to create a new user on the FileZilla Interface ]

3) Mercury:

   Postmaster: Postmaster (postmaster@localhost)
   Administrator: Admin (admin@localhost)

   TestUser: newuser
   Password: wampp

4) WEBDAV:

   User: xampp-dav-unsecure
   Password: ppmax2011
   
5) WordPress:

   User: admin
   Password: FeltHeadwallWight357


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