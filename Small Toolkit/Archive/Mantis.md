[[Active Notes Template]]
## Provided Credentials
---

```

```

```

```

---
## Open Ports

```powershell
PORT     STATE SERVICE REASON         VERSION
80/tcp   open  http    syn-ack ttl 61 Apache httpd 2.4.41 ((Ubuntu))
|_http-server-header: Apache/2.4.41 (Ubuntu)
| http-methods: 
|_  Supported Methods: GET POST OPTIONS HEAD
|_http-favicon: Unknown favicon MD5: 6DC825C260AFEEA86DFCFEE3B99F13BF
|_http-title: Slick - Bootstrap 4 Template
3306/tcp open  mysql   syn-ack ttl 61 MariaDB 5.5.5-10.3.34
| mysql-info: 
|   Protocol: 10
|   Version: 5.5.5-10.3.34-MariaDB-0ubuntu0.20.04.1
|   Thread ID: 51
|   Capabilities flags: 63486
|   Some Capabilities: SupportsCompression, InteractiveClient, SupportsLoadDataLocal, FoundRows, Support41Auth, SupportsTransactions, ODBCClient, LongColumnFlag, IgnoreSigpipes, ConnectWithDatabase, IgnoreSpaceBeforeParenthesis, Speaks41ProtocolNew, DontAllowDatabaseTableColumn, Speaks41ProtocolOld, SupportsAuthPlugins, SupportsMultipleStatments, SupportsMultipleResults
|   Status: Autocommit
|   Salt: HO1HVW37Z?j{KF[tZE+F
|_  Auth Plugin Name: mysql_native_password

```

---
## Software Versions

```powershell

```

---
## Discovered Subdomains

---
## Discovered Credentials

$g_hostname               = 'localhost';
$g_db_type                = 'mysqli';
$g_database_name          = 'bugtracker';
$g_db_username            = 'root';
$g_db_password            = 'SuperSequelPassword';

$g_default_timezone       = 'UTC';

$g_crypto_master_salt     = 'OYAxsrYFCI+xsFw3FNKSoBDoJX4OG5aLrp7rVmOCFjU=';


|  1 | administrator |          | root@localhost      | c7870d0b102cfb2f4916ff04e47b5c6f |       1 |         0 |           90 |           5 |                           0 |                  1 | Tgl-0N5B643JKwIwNgD9s5dKRU_gdBsXawwO7p3ZaGM2ZI4gckyB84AmBRq-IFA7 | 1651296959 |   1651292492 |



---
## Interesting Files/Paths

---
## Attack Ideas

---
## Steps to User.txt


[[Current Affairs Notes Template]]

# Steps to User flag

Run rust scan, ports 80 and 3306 open

3306 doesnt have anything interesting so far, focus on 80

visiting webpage shows a default slick page.

Decide to directory fuzz against ip address

/bugtracker is revealed, showing a mantis bug tracker page

http://192.168.228.204/bugtracker/admin/install.php shows that webpage can interact with sql database

Updating Configuration File (config/config_inc.php)

Google search vaguely suggests that the creds to the sql database is in this file

The goal now is to try to read this file

Search for Mantis arbitrary file read

https://mantisbt.org/bugs/view.php?id=23173

links to 

https://github.com/allyshka/Rogue-MySql-Server/blob/master/roguemysql.php

/var/www/html (webroot)

/var/www/html/bugtracker/config/config_inc.php

gives me creds to db 

in the db, at mantis_user_table, i get administrator creds

hash run through hash-identifier to identify md5

hashcat crack md5 for pw : prayingmantis

https://mantisbt.org/bugs/view.php?id=26091

Follow this POC to achieve RCE

Local.txt in mantis user


---
## Steps to root.txt

After seeing backup.sh, launch pspy to see recurring jobs

creds for mysqldump shows 

mysqldump -u bugtracker -pBugTracker007 bugtracker 

su to mantis using this password

sudo -l shows all/all

sudo -i to become root




---
## User Flag

```

```

## Root Flag

```

```