Full list of 2john tools
```
ls /usr/sbin/*2john /usr/bin/*2john /usr/share/john/*2john 2>/dev/null
```

---
```
john -w=/usr/share/wordlists/rockyou.txt hash.txt
```

```
john --single [filename]
```

```
john --show hash.txt
```
Zip2john
---

```
zip2john [file] > hashes
```

![[Pasted image 20250528032644.png]]

john -w=/usr/share/wordlists/rockyou.txt hashes 

![[Pasted image 20250528032857.png]]

office2john

```
locate office2john.py
```

```
python3 /usr/share/john/office2john.py [filename] > office_hash.txt
```

Crack with wordlist

```
john --wordlist=/usr/share/wordlists/rockyou.txt office_hash.txt
```

---

Shadow.backup

```
john shadow.backup --wordlist=/usr/share/wordlists/rockyou.txt
```

---

keepass2 john.

recovery.kdbx : File version '40000' is currently not supported!

So need a later version of john that can only be simulated through snapd

```
sudo systemctl start snapd.service snapd.socket
```

```
sudo cp /usr/share/wordlists/rockyou.txt .
```

```
snap run john-the-ripper.keepass2john recovery.kdbx >hash
```

```
sudo chown kali:kali rockyou.txt && sudo chmod 664 rockyou.txt && ls -l hash rockyou.txt
```

```
snap run john-the-ripper hash --wordlist=rockyou.txt --format=KeePass
```

---