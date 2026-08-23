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
25/tcp   open  smtp          syn-ack ttl 125 hMailServer smtpd
| smtp-commands: MAILSRV1, SIZE 20480000, AUTH LOGIN, HELP
|_ 211 DATA HELO EHLO MAIL NOOP QUIT RCPT RSET SAML TURN VRFY
80/tcp   open  http          syn-ack ttl 125 Microsoft IIS httpd 10.0
|_http-server-header: Microsoft-IIS/10.0
|_http-title: IIS Windows Server
| http-methods: 
|   Supported Methods: OPTIONS TRACE GET HEAD POST
|_  Potentially risky methods: TRACE
110/tcp  open  pop3          syn-ack ttl 125 hMailServer pop3d
|_pop3-capabilities: TOP UIDL USER
135/tcp  open  msrpc         syn-ack ttl 125 Microsoft Windows RPC
139/tcp  open  netbios-ssn   syn-ack ttl 125 Microsoft Windows netbios-ssn
143/tcp  open  imap          syn-ack ttl 125 hMailServer imapd
|_imap-capabilities: CHILDREN OK QUOTA IMAP4 SORT IMAP4rev1 CAPABILITY NAMESPACE RIGHTS=texkA0001 IDLE completed ACL
445/tcp  open  microsoft-ds? syn-ack ttl 125
587/tcp  open  smtp          syn-ack ttl 125 hMailServer smtpd
| smtp-commands: MAILSRV1, SIZE 20480000, AUTH LOGIN, HELP
|_ 211 DATA HELO EHLO MAIL NOOP QUIT RCPT RSET SAML TURN VRFY
5985/tcp open  http          syn-ack ttl 125 Microsoft HTTPAPI httpd 2.0 (SSDP/UPnP)
|_http-title: Not Found
|_http-server-header: Microsoft-HTTPAPI/2.0
5986/tcp open  ssl/wsmans?   syn-ack ttl 125
|_ssl-date: TLS randomness does not represent time
| ssl-cert: Subject: commonName=Cloudbase-Init WinRM
| Issuer: commonName=Cloudbase-Init WinRM
| Public Key type: rsa
| Public Key bits: 2048
| Signature Algorithm: sha256WithRSAEncryption
| Not valid before: 2026-08-22T10:06:36
| Not valid after:  2036-08-20T10:06:36
| MD5:     82e2 888c 37f0 a145 9b48 5bec a9cb d51c
| SHA-1:   10e6 572a 7622 6061 2a3e 610f 5f59 3837 cc1e a4ff
| SHA-256: af4c cb27 663c 8855 c6c6 2d20 45df 623b 9758 7a1b 6941 7b79 c60d 2af1 5a7f 3e09
| -----BEGIN CERTIFICATE-----
| MIICxjCCAa6gAwIBAgIQQYxzevYDY7BNtv5ljx2nzDANBgkqhkiG9w0BAQsFADAf
| MR0wGwYDVQQDExRDbG91ZGJhc2UtSW5pdCBXaW5STTAeFw0yNjA4MjIxMDA2MzZa
| Fw0zNjA4MjAxMDA2MzZaMB8xHTAbBgNVBAMTFENsb3VkYmFzZS1Jbml0IFdpblJN
| MIIBIjANBgkqhkiG9w0BAQEFAAOCAQ8AMIIBCgKCAQEAzxxhAT3+BgrDnTwPhat2
| KTsHJWxEH8HE+oYly/eFSbng6cGTJ4/oaaOsz4vXgcthNIZpbMtartO5M5rBdFEd
| St+cVwFXXtERyk4BnR8Yt6VqYLtNHtVnATl7qJf3n7wtxIsfNZYnAJJ+eXBx+K6X
| aucAdP/aJjkaUtyEgFhkGfOzAqMFcZFAODb56hzB156uxJxpZOWPKDZRbKiuKiim
| 28i+wnkGgdvKoLwAJiG26XXe/9RGGsvpka7sbWkBS11F7zoeO4WmCeG5iv1W7pSk
| TpexichNg9J478S1jKdC+dQouM9/DRr1G3VxC5KTLIbDFyuzh7MeoGD33jkqWyjw
| xQIDAQABMA0GCSqGSIb3DQEBCwUAA4IBAQCMnJjkfpNMAqrO9HYi6s2+kxNg04/g
| WbgAkYVFLZ82IZqDvZScq65zD87AmBIYEPpTzv9Gs2ZDRacfrL3kwFUFeRf+7X9r
| B1yY/HxkZM5AtAtivud3pBcFhoqY8cTO0UfQYZxc7Rf7JEnJVDJX/sid6y/Jv/BM
| idu7+/AoO18wm5mKZxDpPth+G+aTN6olnbOxcw6h0IEkwQLbrcMhy4ll01WicNBC
| ynzyPO8UUPx3A5weXCRZS27AHSwuhFkHf76t3/hAL2XvrKs4EitWuZvFtGt3KhwZ
| rALyLuQ2C+c2Oes64TuZypNggKMPnCAy2ZmR1rmbCMjnHuyB00x5sOUc
|_-----END CERTIFICATE-----
| tls-alpn: 
|   h2
|_  http/1.1
Service Info: Host: MAILSRV1; OS: Windows; CPE: cpe:/o:microsoft:windows

Host script results:
| p2p-conficker: 
|   Checking for Conficker.C or higher...
|   Check 1 (port 41829/tcp): CLEAN (Couldn't connect)
|   Check 2 (port 61523/tcp): CLEAN (Couldn't connect)
|   Check 3 (port 6032/udp): CLEAN (Timeout)
|   Check 4 (port 55273/udp): CLEAN (Failed to receive data)
|_  0/4 checks are positive: Host is CLEAN or ports are blocked
| smb2-time: 
|   date: 2026-08-23T11:12:09
|_  start_date: N/A
|_clock-skew: 7h59m59s
| smb2-security-mode: 
|   3.1.1: 
|_    Message signing enabled but not required

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