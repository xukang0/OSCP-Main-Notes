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
21/tcp    open  ftp           FileZilla ftpd 0.9.60 beta

CHecked lftp anonymous
CHecked ftp anonymous

22/tcp    open  ssh           OpenSSH for_Windows_8.1 (protocol 2.0)

135/tcp   open  msrpc         Microsoft Windows RPC
RPCClient tried (both)

139/tcp   open  netbios-ssn   Microsoft Windows netbios-ssn
445/tcp   open  microsoft-ds?

smbmap
enum4linux
enum4linuxNG 
tried


3389/tcp  open  ms-wbt-server Microsoft Terminal Services
| rdp-ntlm-info: 
|   Target_Name: NICKEL
|   NetBIOS_Domain_Name: NICKEL
|   NetBIOS_Computer_Name: NICKEL
|   DNS_Domain_Name: nickel
|   DNS_Computer_Name: nickel
|   Product_Version: 10.0.18362
|_  System_Time: 2026-08-02T03:45:23+00:00
|_ssl-date: 2026-08-02T03:46:29+00:00; 0s from scanner time.
| ssl-cert: Subject: commonName=nickel
| Not valid before: 2026-08-01T03:41:14
|_Not valid after:  2027-01-31T03:41:14


5040/tcp  open  unknown
Nothing

7680/tcp  open  pando-pub?
Nothing

8089/tcp  open  http          Microsoft HTTPAPI httpd 2.0 (SSDP/UPnP)
DevOps Dashboard

33333/tcp open  http          Microsoft HTTPAPI httpd 2.0 (SSDP/UPnP)
Invalid Token

49664/tcp open  msrpc         Microsoft Windows RPC
49665/tcp open  msrpc         Microsoft Windows RPC
49666/tcp open  msrpc         Microsoft Windows RPC
49667/tcp open  msrpc         Microsoft Windows RPC
49668/tcp open  msrpc         Microsoft Windows RPC
49669/tcp open  msrpc         Microsoft Windows RPC

```

8089 DeevOps Dashboard
http://169.254.144.247:33333/list-current-deployments?
http://169.254.144.247:33333/list-running-procs?
http://169.254.144.247:33333/list-active-nodes?

curl -X POST -H "Content-Length:0" http://192.168.107.99:33333/list-active-nodes


33333 Invalid token

5040,7680 check

---
## Software Versions

```powershell
Windows 10
```

---
## Discovered Subdomains

---
## Discovered Credentials

name        : cmd.exe
commandline : cmd.exe C:\windows\system32\DevTasks.exe --deploy C:\work\dev.yaml --user ariah -p 
              "Tm93aXNlU2xvb3BUaGVvcnkxMzkK" --server nickel-dev --protocol ssh

User : ariah
Password : Tm93aXNlU2xvb3BUaGVvcnkxMzkK (Base64)
Password : NowiseSloopTheory139
Protocol : SSH 

---
## Interesting Files/Paths

---
## Attack Ideas

---
## Steps to User.txt

Clicking on each link directed me to a different host as shown below

Press enter or click to view image in full size

![](https://miro.medium.com/v2/resize:fit:700/1*Z_Bh8fJy1a-Jlqv_sXtVvQ.png)

The IP address 169.254.x.y is not the same as of the machine. This might be hardcoded. The port 33333 is also avaiable on my target machine. So I will try to connect to these links but using the IP address of my target machine

I used curl for this

curl http://192.168.208.99:33333/list-current-deployments  
curl http://192.168.208.99:33333/list-running-procs?  
curl http://192.168.208.99:33333/list-active-nodes

I got an error message as shown below

Press enter or click to view image in full size

![](https://miro.medium.com/v2/resize:fit:700/1*vFkjpuKSZRlySEG5HYpk4Q.png)

This means that the GET method is not supported, what about the POST method then?, Lets try it

curl -X POST -H "Content-Type:html/txt" http://192.168.208.99:33333/list-current-deployments

Press enter or click to view image in full size

![](https://miro.medium.com/v2/resize:fit:700/1*U50eFjAL3LeeBv242URU9Q.png)

It clearly states that Content-Length is needed, so I added it

Press enter or click to view image in full size

![](https://miro.medium.com/v2/resize:fit:700/1*6kPg6grCurma-wL4BBhEaA.png)

For this link, it returned nothing, so I tried it with the other links. And for the running-processes it return a list of the running process

Press enter or click to view image in full size

![](https://miro.medium.com/v2/resize:fit:700/1*Wc9xD_7TOjkWq6WHLu1jzQ.png)

Going through the list, I found a process that connects to SSH and shows the username and obfuscated password

Press enter or click to view image in full size

![](https://miro.medium.com/v2/resize:fit:700/1*VRuXOsjqgxhgYUndt0xZmQ.png)

I used Cyberchef (magic) and the password is base64 encoded

![](https://miro.medium.com/v2/resize:fit:590/1*EyMr0he-4liPaXX0Wc1VvA.png)

I used now these creds to connect to SSH

---
## Steps to root.txt

---
## User Flag

```

```

## Root Flag

```

```