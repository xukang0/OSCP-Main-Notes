[[Active Notes Template]]
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

## Discovered Credentials

name        : cmd.exe
commandline : cmd.exe C:\windows\system32\DevTasks.exe --deploy C:\work\dev.yaml --user ariah -p 
              "Tm93aXNlU2xvb3BUaGVvcnkxMzkK" --server nickel-dev --protocol ssh

User : ariah
Password : Tm93aXNlU2xvb3BUaGVvcnkxMzkK (Base64)
Password : NowiseSloopTheory139
Protocol : SSH 

## Steps to User.txt

Clicking on each link directed me to a different host as shown below

 

![](https://miro.medium.com/v2/resize:fit:700/1*Z_Bh8fJy1a-Jlqv_sXtVvQ.png)

The IP address 169.254.x.y is not the same as of the machine. This might be hardcoded. The port 33333 is also avaiable on my target machine. So I will try to connect to these links but using the IP address of my target machine

I used curl for this

curl http://192.168.208.99:33333/list-current-deployments  
curl http://192.168.208.99:33333/list-running-procs?  
curl http://192.168.208.99:33333/list-active-nodes

I got an error message as shown below

 

![](https://miro.medium.com/v2/resize:fit:700/1*vFkjpuKSZRlySEG5HYpk4Q.png)

This means that the GET method is not supported, what about the POST method then?, Lets try it

curl -X POST -H "Content-Type:html/txt" http://192.168.208.99:33333/list-current-deployments

 

![](https://miro.medium.com/v2/resize:fit:700/1*U50eFjAL3LeeBv242URU9Q.png)

It clearly states that Content-Length is needed, so I added it

![](https://miro.medium.com/v2/resize:fit:700/1*6kPg6grCurma-wL4BBhEaA.png)

For this link, it returned nothing, so I tried it with the other links. And for the running-processes it return a list of the running process

![](https://miro.medium.com/v2/resize:fit:700/1*Wc9xD_7TOjkWq6WHLu1jzQ.png)

Going through the list, I found a process that connects to SSH and shows the username and obfuscated password

![](https://miro.medium.com/v2/resize:fit:700/1*VRuXOsjqgxhgYUndt0xZmQ.png)

I used Cyberchef (magic) and the password is base64 encoded

![](https://miro.medium.com/v2/resize:fit:590/1*EyMr0he-4liPaXX0Wc1VvA.png)

I used now these creds to connect to SSH

---
## Steps to root.txt


I check users (net user), OS (systeminfo), intersting files and found FTP folder. Inside the folder there was a Pdf file

![](https://miro.medium.com/v2/resize:fit:700/1*Wz6WciZ8pisPUtlLxe9ppQ.png)

Using SCP, I downloaded the file to Kali and tried to open it, but it was password protected. I used Pdfcrack to crack the password and was successful

![](https://miro.medium.com/v2/resize:fit:700/1*DoaB4NJY_-OHZmRcJZnEvw.png)

I used the discovered password to open the file and got this output


![](https://miro.medium.com/v2/resize:fit:700/1*aS5T_kBXT46qFkWKZAiTBQ.png)

It point to a web service on the standard port 80. But form nmap’s output, port 80 was not open. So I need to check of port 80 is locally open.


![](https://miro.medium.com/v2/resize:fit:700/1*jke39cQVj6pe6NhXIm2T-w.png)

Netstat shows that port 80 is open. This means that the port is only accessible locally (from within the machine), so I used curl to access the web

![](https://miro.medium.com/v2/resize:fit:700/1*5jGh8HYo9QgJBZlisUS3qA.png)

No, I will see if I can pass a command as a parameter

![](https://miro.medium.com/v2/resize:fit:700/1*Mju9KJMZny4EIFkDom5KjA.png)

Good, so this means that the passed command will run as system.

The attack vector here is to run a shell, but first I will need to check where this command run from.

![](https://miro.medium.com/v2/resize:fit:700/1*q1qXUWB_izxxROOQBGmPOA.png)

I do not seem to have writing permission on system32, so cannot copy anything into this folder

![](https://miro.medium.com/v2/resize:fit:700/1*CEE_fA1vygPaFtX_y6vVuA.png)

I tried to move within the system files but it seems that the payload is should be encoded

 

![](https://miro.medium.com/v2/resize:fit:700/1*Jh-lVXBnvg_clZ1yJWRAzQ.png)

I used online encoder

![](https://miro.medium.com/v2/resize:fit:571/1*WvotiTDDqDVMDopkLzLBAw.png)

And it worked


![](https://miro.medium.com/v2/resize:fit:700/1*OoqurADs-VeRVzExdC9jjw.png)

Now, I uploaded nc.exe to Ariah’s home directory and form there, I will need to move there first

![](https://miro.medium.com/v2/resize:fit:315/1*V6oiBS91e60tqXpyz3YL9g.png)

 

![](https://miro.medium.com/v2/resize:fit:700/1*WsJ_yNTuw9i9KMLyhExixw.png)

Now, Ill try to run nc

![](https://miro.medium.com/v2/resize:fit:597/1*zOcq6Yc6i5muQCVD_EYNkw.png)

 

![](https://miro.medium.com/v2/resize:fit:700/1*8irkAnndL2w3t8Xc3EHerg.png)

And I got a system shell

 

![](https://miro.medium.com/v2/resize:fit:700/1*R3pZfje9hwCxeZ5XbkyafA.png)

[](https://medium.com/m/signin?actionUrl=https%3A%2F%2Fmedium.com%2F_%2Frepost%2Fp%2Fc41e273146bf&operation=register&redirect=https%3A%2F%2Fmedium.com%2F%40mahdi_78420%2Fnickel-walkthrough-practice-tj-c41e273146bf&user=Dr+Mahdi+Aiash&userId=288e2a3f1404&source=---footer_actions--c41e273146bf---------------------repost_footer------------------)

[](https://medium.com/m/signin?actionUrl=https%3A%2F%2Fmedium.com%2F_%2Fbookmark%2Fp%2Fc41e273146bf&operation=register&redirect=https%3A%2F%2Fmedium.com%2F%40mahdi_78420%2Fnickel-walkthrough-practice-tj-c41e273146bf&source=---footer_actions--c41e273146bf---------------------bookmark_footer------------------)

[](https://medium.com/@mahdi_78420?source=post_page---post_author_info--c41e273146bf---------------------------------------)
---
## User Flag

```

```

## Root Flag

```

```