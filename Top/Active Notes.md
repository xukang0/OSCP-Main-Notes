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
21/tcp   open  ftp     ProFTPD 1.3.5b


22/tcp   open  ssh     OpenSSH 7.4p1 Debian 10+deb9u7 (protocol 2.0)
| ssh-hostkey: 
|   2048 aa:77:6f:b1:ed:65:b5:ad:14:64:40:d2:24:d3:9c:0d (RSA)
|   256 a9:b4:4f:61:2e:2d:9d:4c:48:15:fe:70:8e:fa:af:b3 (ECDSA)
|_  256 92:56:eb:af:c9:34:af:ea:a1:cf:9f:e1:90:dd:2f:61 (ED25519)


2222/tcp open  ssh     Dropbear sshd 2016.74 (protocol 2.0)


3000/tcp open  http    Golang net/http server
|_http-title: Gitea: Git with a cup of tea
| fingerprint-strings: 
|   GenericLines, Help: 
|     HTTP/1.1 400 Bad Request
|     Content-Type: text/plain; charset=utf-8
|     Connection: close
|     Request
|   GetRequest: 
|     HTTP/1.0 200 OK
|     Content-Type: text/html; charset=UTF-8
|     Set-Cookie: lang=en-US; Path=/; Max-Age=2147483647
|     Set-Cookie: i_like_gitea=6a2dda89e6df6e21; Path=/; HttpOnly
|     Set-Cookie: _csrf=JVbV5gFAVQnxGhcF59w0VMxP8EY6MTc3OTg5NTUwODUzMDE0Mjk3Nw%3D%3D; Path=/; Expires=Thu, 28 May 2026 15:25:08 GMT; HttpOnly
|     X-Frame-Options: SAMEORIGIN
|     Date: Wed, 27 May 2026 15:25:08 GMT
|     <!DOCTYPE html>
|     <html>
|     <head data-suburl="">
|     <meta charset="utf-8">
|     <meta name="viewport" content="width=device-width, initial-scale=1">
|     <meta http-equiv="x-ua-compatible" content="ie=edge">
|     <title>Gitea: Git with a cup of tea</title>
|     <link rel="manifest" href="/manifest.json" crossorigin="use-credentials">
|     <script>
|     ('serviceWorker' in navigator) {
|     window.addEventListener('load', function() {
|     navigator.serviceWorker.register('/serviceworker.js').then(function(registration) {
|   HTTPOptions: 
|     HTTP/1.0 404 Not Found
|     Content-Type: text/html; charset=UTF-8
|     Set-Cookie: lang=en-US; Path=/; Max-Age=2147483647
|     Set-Cookie: i_like_gitea=b5f80e34c4e16368; Path=/; HttpOnly
|     Set-Cookie: _csrf=hfKjgHeQ0t_iDaB6zHpFc1bvWH86MTc3OTg5NTUwODU5NTAyNTgzMw%3D%3D; Path=/; Expires=Thu, 28 May 2026 15:25:08 GMT; HttpOnly
|     X-Frame-Options: SAMEORIGIN
```


---
## Software Versions

```powershell

```


---
## Discovered Subdomains




---
## Discovered Credentials


| Username | Password | Notes |
| -------- | -------- | ----- |
|          |          |       |

---
## Attack Angles





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