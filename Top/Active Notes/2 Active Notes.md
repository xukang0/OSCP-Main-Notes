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
22/tcp    open  ssh           syn-ack ttl 125 OpenSSH for_Windows_8.1 (protocol 2.0)
|_ssh-ed25519 AAAAC3NzaC1lZDI1NTE5AAAAICyZUVdHOqTpEFyvELlmc7sCN1XFXQo7RdZdTRTPO2uJ
135/tcp   open  msrpc         syn-ack ttl 125 Microsoft Windows RPC
139/tcp   open  netbios-ssn   syn-ack ttl 125 Microsoft Windows netbios-ssn
445/tcp   open  microsoft-ds? syn-ack ttl 125
5040/tcp  open  unknown       syn-ack ttl 125
5985/tcp  open  http          syn-ack ttl 125 Microsoft HTTPAPI httpd 2.0 (
5986/tcp  open  ssl/wsmans?   syn-ack ttl 125
|_-----END CERTIFICATE-----
7680/tcp  open  pando-pub?    syn-ack ttl 125
8000/tcp  open  http          syn-ack ttl 125 Microsoft HTTPAPI httpd 2.0 
47001/tcp open  http          syn-ack ttl 125 Microsoft HTTPAPI httpd 2.0
49664/tcp open  msrpc         syn-ack ttl 125 Microsoft Windows RPC
49665/tcp open  msrpc         syn-ack ttl 125 Microsoft Windows RPC
49666/tcp open  msrpc         syn-ack ttl 125 Microsoft Windows RPC
49667/tcp open  msrpc         syn-ack ttl 125 Microsoft Windows RPC
49668/tcp open  msrpc         syn-ack ttl 125 Microsoft Windows RPC
49669/tcp open  msrpc         syn-ack ttl 125 Microsoft Windows RPC
49671/tcp open  msrpc         syn-ack ttl 125 Microsoft Windows RPC
49703/tcp open  msrpc         syn-ack ttl 125 Microsoft Windows RPC

```

---
## Software Versions

```powershell

```

---
## Discovered Subdomains

---
## Discovered Credentials

INSERT OR IGNORE INTO 'partners'('id', 'name', 'password', 'desc') VALUES (1, 'ecorp', '7007296521223107d3445ea0db5a04f9', '-');
INSERT OR IGNORE INTO 'partners'('id', 'name', 'password', 'desc') VALUES (2, 'support', '26231162520c611ccabfb18b5ae4dff2', 'support account for internal use');
INSERT OR IGNORE INTO 'partners'('id', 'name', 'password', 'desc') VALUES (3, 'bcorp', 'e7966b31d1cad8a83f12ecec236c384c', '-');
INSERT OR IGNORE INTO 'partners'('id', 'name', 'password', 'desc') VALUES (4, 'acorp', 'df5fb539ff32f7fde5f3c05d8c8c1a6e', '-');

cloudbase-init 91f8e3711ffdaa895cd01a89762a727e : unknown
ms01$ fc7c8431a3fa6d042828a5d1b49fe1ab : unknown
support : d9358122015c5b159574a88b3c0d2071 :Freedom1
administrator : 3c4495bbd678fac8c9d218be4f2bbc7b : December31

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