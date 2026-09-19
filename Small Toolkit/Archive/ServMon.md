[[NSclient++]], Windows, HTB, NVMS 100, searchsploit, directory traversal, 


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
Open 10.129.227.77:22
Open 10.129.227.77:21
Open 10.129.227.77:80
Open 10.129.227.77:135
Open 10.129.227.77:139
Open 10.129.227.77:445
Open 10.129.227.77:5666
Open 10.129.227.77:6063
Open 10.129.227.77:6699
Open 10.129.227.77:8443

```

---
## Software Versions

```powershell
OS: Windows 10, Windows Server 2019, Windows Server 2016
OS version: '10.0'
OS release: '1809'
OS build: '17763
```

---
## Discovered Subdomains

---
## Discovered Credentials

1nsp3ctTh3Way2Mars!

Th3r34r3To0M4nyTrait0r5!

B3WithM30r4ga1n5tMe

L1k3B1gBut7s@W0rk

0nly7h3y0unGWi11F0l10w

IfH3s4b0Utg0t0H1sH0me

Gr4etN3w5w17hMySk1Pa5$

---
## Interesting Files/Paths

---
## Attack Ideas

---

[[Current Affairs Notes Template]]

# Steps to User flag

RPC 135 and SMB 445 open means this is a windows box

135RPC X
139 SMB Only get OS information
21 FTP allows anonymous login. There is a confidential.txt and Notes to do. There are some notes by Nathan regarding his creds

NVMS 100 has a directory traversal vulnerability, since nathan mentions that he has saved passwords on his desktop, try a blind guess of the path

/../../../../../../../../../../../../Users/nathan/Desktop/passwords.txt

I get a random list of passwords to try

Use nxc to see which one is the valid password

nxc returns this creds as valid nadine:L1k3B1gBut7s@W0rk

nxc tells me these creds work for SSH

SSH into nadine and get user flag on her desktop

---

Access to nathan is denied

There is a folder in root called RecData containing db3 files

used [[SCP]] to download both files over to my kali

RecordInfoDB.db3-journal is empty, RecordInfoDB.db3-journal is a sqlite 3.X database

nsclient searchsploit priv esc tells me to read C:\Program Files\NSClient++\nsclient.ini, I see an undocumented password ew2x6SsGTxjRwXOT

We need to local port forward using sshpass [[22 SSH]] so we can access port 8443 internal web server

127.0.0.1:8443 with the password allows me to login as nadine into dashboard

nsclient box https://0xdf.gitlab.io/2020/06/20/htb-servmon.html#website---tcp-80

https://viperone.gitbook.io/pentest-everything/writeups/hackthebox/windows-machines/servmon

## User Flag

```

```

## Root Flag

```

```