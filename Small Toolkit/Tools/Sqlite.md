We can now open the database using sqlite3 .
```
sqlite3 sql.db
```

```
.tables
```

```
.recover
```

```
select * from users;
```

---

```
Get-ChildItem -Path C:\ -Filter mysql.exe -Recurse -ErrorAction SilentlyContinue
```

.sql

```
mysql -u username -p database_name < file.sql
```

  
4. SQLite  
SQLite is different because it's typically an embedded database rather than a database server listening on a port.  
Open a database file:  

sqlite3 database.db

  
Basic commands:  

.tables

  

.schema

  

.schema table_name

  

SELECT * FROM table_name;

  
Show database configuration:  

.databases

  
Exit:  

.quit

  
SQLite databases commonly appear during web application enumeration when you discover files such as:  

database.db
db.sqlite3
users.db

  
  
Quick reference  
  
For OSCP, I'd memorize the **connection syntax, database enumeration, table enumeration, schema inspection, basic SELECT queries, and how to exit**. That's usually more valuable than memorizing extensive SQL syntax.