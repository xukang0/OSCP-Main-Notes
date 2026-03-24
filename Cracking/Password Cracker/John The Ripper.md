```
john -w=/usr/share/wordlists/rockyou.txt hash.txt
```

```
john --single [filename]
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

