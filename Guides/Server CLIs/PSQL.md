psql -U christine -h localhost -p 1234

![[Pasted image 20250520021305.png]]

In order to list the existing databases, we can execute the
\l command, short for \list 
```
\l
```

![[Pasted image 20250520021353.png]]

Five rows are returned, including a database with the ominous name secrets .

Using the \c command, short for \connect , we can select a database and proceed to interact with its tables.
```
\c {database_name}
```

![[Pasted image 20250520021458.png]]

Finally, we can list the database's tables using the \dt command, and dump its contents using the conventional SQL SELECT query.
```
\dt
```

![[Pasted image 20250520021526.png]]
```
SELECT * FROM flag;
```

![[Pasted image 20250520021551.png]]