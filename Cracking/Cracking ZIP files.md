```
zip2john [file].zip > zip.hash
```

```
cat zip.hash
```

John the ripper to crack the hash

```
john --wordlist=rockyou.txt zip.hash
```

```
john zip.hash --show
```