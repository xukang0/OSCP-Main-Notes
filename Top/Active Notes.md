[IP]
```dataviewjs
const page = dv.page("Templater/IP");const ip = page?.IP ?? "NO IP FOUND";

const command = `${ip}`;

dv.paragraph("```bash\n" + command + "\n```");
```
Web Address
```dataviewjs
const page = dv.page("Templater/IP");const ip = page?.IP ?? "NO IP FOUND";

const command = `http://${ip}/`;

dv.paragraph("```bash\n" + command + "\n```");
```
Editing Box

```

```

wget from local python server

```dataviewjs
const page = dv.page("Templater/IP");const KaliIP = page?.["KALI IP"] ?? "NO KALI IP FOUND";

const command = `wget http://${KaliIP}:8000/[file]`;

dv.paragraph("```bash\n" + command + "\n```");
```


## Provided Credentials
---

| Username | Password | Notes |
| -------- | -------- | ----- |
|          |          |       |

---


## Open Ports
---

| Port                                                                                                                                                                                                                                                                                                                                                                                                              | Service | Notes |
| ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ------- | ----- |
| 22                                                                                                                                                                                                                                                                                                                                                                                                                | ssh     |       |
| 80                                                                                                                                                                                                                                                                                                                                                                                                                | http    |       |
| PORT      STATE         SERVICE<br>68/udp    open\|filtered dhcpc<br>161/udp   open          snmp<br>497/udp   open\|filtered retrospect<br>593/udp   open\|filtered http-rpc-epmap<br>631/udp   open\|filtered ipp<br>1023/udp  open\|filtered unknown<br>1812/udp  open\|filtered radius<br>1813/udp  open\|filtered radacct<br>5632/udp  open\|filtered pcanywherestat<br>49200/udp open\|filtered unknown<br> |         |       |

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