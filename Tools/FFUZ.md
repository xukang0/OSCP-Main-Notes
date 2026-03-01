```
locate common.txt
```

```
ffuf -u http://web1337.inlanefreight.htb:<PORT>/FUZZ -w /YOUR PATH/common.txt:FUZZ -e .html -v
```

Wake the server up using curl

```
curl http://web1337.inlanefreight.htb:40499/admin_h1dd3n -I
```
