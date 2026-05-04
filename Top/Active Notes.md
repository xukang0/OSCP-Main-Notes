IP::   10.129.35.38

| Machine | IP Address | Notes |
| ------- | ---------- | ----- |
|         |            |       |

```dataviewjs
const page = dv.page("Synced OSCP Notes/Top/Active Notes");const ip = page?.IP ?? "NO IP FOUND";

const command = `${ip}`;

dv.paragraph("```bash\n" + command + "\n```");
```
KALI IP::  10.10.17.59
```dataviewjs
const page = dv.page("Synced OSCP Notes/Top/Active Notes");const KaliIP = page?.["KALI IP"] ?? "NO KALI IP FOUND";

const command = `${KaliIP}`;

dv.paragraph("```bash\n" + command + "\n```");
```
Web Address
```dataviewjs
const page = dv.page("Synced OSCP Notes/Top/Active Notes");const ip = page?.IP ?? "NO IP FOUND";

const command = `http://${ip}/`;

dv.paragraph("```bash\n" + command + "\n```");
```
Discovered Web Domain::   EXAMPLECOM
```dataviewjs
const page = dv.page("Synced OSCP Notes/Top/Active Notes");
const discoveredDomain = page?.["Discovered Web Domain"] ?? "NO DOMAIN FOUND";

const command = `http://${discoveredDomain}/`;

dv.paragraph("```bash\n" + command + "\n```");
```
[[Editing Page]]

wget from local python server
```dataviewjs
const page = dv.page("Synced OSCP Notes/Top/Active Notes");const KaliIP = page?.["KALI IP"] ?? "NO KALI IP FOUND";

const command = `wget http://${KaliIP}:8000/[file]`;

dv.paragraph("```bash\n" + command + "\n```");
```
## Provided Credentials
---

```

```

```

```

---
## Software Versions







---



## Open Ports
---
PORT    STATE SERVICE  VERSION
22/tcp  open  ssh      OpenSSH 9.2p1 Debian 2+deb12u7 (protocol 2.0)
80/tcp  open  http     Jetty
443/tcp open  ssl/http Jetty

| Port | Service | Notes |
| ---- | ------- | ----- |
|      |         |       |
49/udp    open|filtered tacacs
53/udp    open|filtered domain
68/udp    open|filtered dhcpc
80/udp    open|filtered http
161/udp   open|filtered snmp
514/udp   open|filtered syslog
1022/udp  open|filtered exp2
1027/udp  open|filtered unknown
1433/udp  open|filtered ms-sql-s
1645/udp  open|filtered radius
1719/udp  open|filtered h323gatestat
2222/udp  open|filtered msantipiracy
3456/udp  open|filtered IISrpc-or-vat
30718/udp open|filtered unknown
49154/udp open|filtered unknown

ss -tlpn
State  Recv-Q Send-Q Local Address:Port  Peer Address:PortProcess                          
LISTEN 0      128          0.0.0.0:22         0.0.0.0:*                                    
LISTEN 0      80         127.0.0.1:3306       0.0.0.0:*     mysql                               
LISTEN 0      50           0.0.0.0:80         0.0.0.0:*    users:(("java",pid=3560,fd=327))
LISTEN 0      128        127.0.0.1:54321      0.0.0.0:*                                    
LISTEN 0      50           0.0.0.0:443        0.0.0.0:*    users:(("java",pid=3560,fd=331))
LISTEN 0      256          0.0.0.0:6661       0.0.0.0:*    users:(("java",pid=3560,fd=335))
LISTEN 0      128             [::]:22            [::]:*                                    

49190/udp open|filtered unknown
---

## Discovered Subdomains
---


---

## Discovered Credentials
---

| Username | Password | Notes |
| -------- | -------- | ----- |
|          |          |       |

---

## Attack Angles
---


---

## User Flag

```

```

## Root Flag

```

```