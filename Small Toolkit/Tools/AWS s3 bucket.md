```
aws configure
```

See bucket
```
aws s3 ls --endpoint-url http://facts.htb:54321
```

Go into a folder
```
aws s3 ls s3://randomfacts --endpoint-url http://facts.htb:54321
```

Read file
```
aws s3 cp s3://randomfacts/Users.txt - --endpoint-url http://facts.htb:54321
```