```
file GZIP.gzip 
```

RESULT

```shell-session
GZIP.gzip: openssl enc'd data with salted password
```

For loop crack

```
for i in $(cat rockyou.txt);do openssl enc -aes-256-cbc -d -in GZIP.gzip -k $i 2>/dev/null| tar xz;done
```