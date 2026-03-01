```shell-session
ffuf -w /usr/share/seclists/Discovery/Web-Content/directory-list-2.3-small.txt:FUZZ -u http://SERVER_IP:PORT/FUZZ -recursion -recursion-depth 1 -e .php -v
```

-w wordlist
-u target
-recursion
-recursion depth
1 - default
2 - deeper
3 - deepest
-e extension format
-v verbose

```
PORT=56270;ffuf -w /usr/share/seclists/Discovery/Web-Content/directory-list-2.3-small.txt:FUZZ -u http://faculty.academy.htb:$PORT/FUZZ -recursion -recursion-depth 1 -e ".php,.phps,.php7" -v -fc 403 -fs 0
```