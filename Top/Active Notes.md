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

| Port                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                           | Service | Notes |
| -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ------- | ----- |
| 53/tcp   open  domain        Simple DNS Plus<br>80/tcp   open  http          Microsoft IIS httpd 10.0<br>88/tcp   open  kerberos-sec  Microsoft Windows Kerberos (server time: 2026-03-12 13:07:00Z)<br>135/tcp  open  msrpc         Microsoft Windows RPC<br>139/tcp  open  netbios-ssn   Microsoft Windows netbios-ssn<br>389/tcp  open  ldap          Microsoft Windows Active Directory LDAP (Domain: return.local0., Site: Default-First-Site-Name)<br>445/tcp  open  microsoft-ds?<br>464/tcp  open  kpasswd5?<br>593/tcp  open  ncacn_http    Microsoft Windows RPC over HTTP 1.0<br>636/tcp  open  tcpwrapped<br>3268/tcp open  ldap          Microsoft Windows Active Directory LDAP (Domain: return.local0., Site: Default-First-Site-Name)<br>3269/tcp open  tcpwrapped<br>5985/tcp open  http          Microsoft HTTPAPI httpd 2.0 (SSDP/UPnP)<br> |         |       |

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