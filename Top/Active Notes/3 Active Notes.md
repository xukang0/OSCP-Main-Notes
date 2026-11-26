[[Active Notes Template]]
## Provided Credentials
---

```
r.andrews
```

```
BusyOfficeWorker890
```

---
## Open Ports

```powershell
┌──(kali㉿kali)-[~/…/OSCP/AD/MS01/enum]
└─$ sudo rustscan -a 192.168.123.206 -b 500 --ulimit 5000 -- -sC -sV -Pn -oN 192.168.123.206_Fast_Rustscan
[sudo] password for kali: 
.----. .-. .-. .----..---.  .----. .---.   .--.  .-. .-.
| {}  }| { } |{ {__ {_   _}{ {__  /  ___} / {} \ |  `| |
| .-. \| {_} |.-._} } | |  .-._} }\     }/  /\  \| |\  |
`-' `-'`-----'`----'  `-'  `----'  `---' `-'  `-'`-' `-'
The Modern Day Port Scanner.
________________________________________
: http://discord.skerritt.blog         :
: https://github.com/RustScan/RustScan :
 --------------------------------------
😵 https://admin.tryhackme.com

[~] The config file is expected to be at "/root/.rustscan.toml"
[~] Automatically increasing ulimit value to 5000.

Scanning 192.168.123.206 [19 ports]
Discovered open port 3306/tcp on 192.168.123.206
Discovered open port 135/tcp on 192.168.123.206
Discovered open port 445/tcp on 192.168.123.206
Discovered open port 80/tcp on 192.168.123.206
Discovered open port 3389/tcp on 192.168.123.206
Discovered open port 139/tcp on 192.168.123.206
Discovered open port 443/tcp on 192.168.123.206
Discovered open port 5040/tcp on 192.168.123.206
Discovered open port 49668/tcp on 192.168.123.206
Discovered open port 49671/tcp on 192.168.123.206
Discovered open port 49667/tcp on 192.168.123.206
Discovered open port 49672/tcp on 192.168.123.206
Discovered open port 49670/tcp on 192.168.123.206
Discovered open port 5985/tcp on 192.168.123.206
Discovered open port 49665/tcp on 192.168.123.206
Discovered open port 49666/tcp on 192.168.123.206
Discovered open port 49669/tcp on 192.168.123.206
Discovered open port 49664/tcp on 192.168.123.206
Discovered open port 47001/tcp on 192.168.123.206

PORT      STATE SERVICE       REASON          VERSION
80/tcp    open  http          syn-ack ttl 127 Apache httpd 2.4.58 ((Win64) OpenSSL/3.1.3 PHP/8.2.35)
|_http-server-header: Apache/2.4.58 (Win64) OpenSSL/3.1.3 PHP/8.2.35
| http-methods: 
|_  Supported Methods: GET HEAD POST OPTIONS
|_http-title: Home - OffSec NIC
| http-cookie-flags: 
|   /: 
|     PHPSESSID: 
|_      httponly flag not set
135/tcp   open  msrpc         syn-ack ttl 127 Microsoft Windows RPC
139/tcp   open  netbios-ssn   syn-ack ttl 127 Microsoft Windows netbios-ssn
443/tcp   open  ssl/http      syn-ack ttl 127 Apache httpd 2.4.58 ((Win64) OpenSSL/3.1.3 PHP/8.2.35)
|_http-title: Home - OffSec NIC
| http-cookie-flags: 
|   /: 
|     PHPSESSID: 
|_      httponly flag not set
|_http-server-header: Apache/2.4.58 (Win64) OpenSSL/3.1.3 PHP/8.2.35
445/tcp   open  microsoft-ds? syn-ack ttl 127
3306/tcp  open  mysql         syn-ack ttl 127 MariaDB 10.3.23 or earlier (unauthorized)
3389/tcp  open  ms-wbt-server syn-ack ttl 127
| ssl-cert: Subject: commonName=WS26.oscp.exam
| Issuer: commonName=WS26.oscp.exam
| rdp-ntlm-info: 
|   Target_Name: OSCP
|   NetBIOS_Domain_Name: OSCP
|   NetBIOS_Computer_Name: WS26
|   DNS_Domain_Name: oscp.exam
|   DNS_Computer_Name: WS26.oscp.exam
|   DNS_Tree_Name: oscp.exam
|   Product_Version: 10.0.26100
|_  System_Time: 2026-11-26T09:16:28+00:00
5040/tcp  open  unknown       syn-ack ttl 127
5985/tcp  open  http          syn-ack ttl 127 Microsoft HTTPAPI httpd 2.0 
47001/tcp open  http          syn-ack ttl 127 Microsoft HTTPAPI httpd 2.0 (SSDP/UPnP)
|_http-server-header: Microsoft-HTTPAPI/2.0
|_http-title: Not Found
49664/tcp open  msrpc         syn-ack ttl 127 Microsoft Windows RPC
49665/tcp open  msrpc         syn-ack ttl 127 Microsoft Windows RPC
49666/tcp open  msrpc         syn-ack ttl 127 Microsoft Windows RPC
49667/tcp open  msrpc         syn-ack ttl 127 Microsoft Windows RPC
49668/tcp open  msrpc         syn-ack ttl 127 Microsoft Windows RPC
49669/tcp open  msrpc         syn-ack ttl 127 Microsoft Windows RPC
49670/tcp open  msrpc         syn-ack ttl 127 Microsoft Windows RPC
49671/tcp open  msrpc         syn-ack ttl 127 Microsoft Windows RPC
49672/tcp open  msrpc         syn-ack ttl 127 Microsoft Windows RPC

```

---
## Software Versions

```powershell

```

---
## Discovered Subdomains

---
## Discovered Credentials

mssql : qazwsx

r.andrews : BusyOfficeWorker890

Administrator : aad3b435b51404eeaad3b435b51404ee:2a00a0a55d5a916e79c91ad30e770715

INSERT INTO users (email, password, first_name, last_name, phone, company, account_type, email_verified) VALUES
('admin@offsecnic.local', '$2y$10$92IXUNpkjO0rOQ5byMi.Ye4oKoEa3Ro9llC/.og/at2.uheWG/igi' : password, 'Admin', 'User', '+1-415-555-0100', 'OffSec NIC', 'enterprise', TRUE),
('john.doe@example.com', '$2y$10$92IXUNpkjO0rOQ5byMi.Ye4oKoEa3Ro9llC/.og/at2.uheWG/igi', 'John', 'Doe', '+1-555-123-4567', 'Acme Corp', 'premium', TRUE);

   ServiceName              :  HOST/SRV22.OSCP.EXAM
    ServiceRealm             :  OSCP.EXAM
    UserName                 :  WS26$
    UserRealm                :  OSCP.EXAM
    StartTime                :  11/26/2026 7:32:19 AM
    EndTime                  :  11/26/2026 11:05:32 AM
    RenewTill                :  12/3/2026 1:05:32 AM
    Flags                    :  name_canonicalize, pre_authent, renewable, forwardable
    KeyType                  :  aes256_cts_hmac_sha1
    Base64(key)              :  vntKWndqEq/ygOHE2SEduoMSTqd9S12PvY2De/y4vxw=
    Base64EncodedTicket   :

      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


    ServiceName              :  cifs/SRV22.OSCP.EXAM
    ServiceRealm             :  OSCP.EXAM
    UserName                 :  WS26$
    UserRealm                :  OSCP.EXAM
    StartTime                :  11/26/2026 7:32:19 AM
    EndTime                  :  11/26/2026 11:05:32 AM
    RenewTill                :  12/3/2026 1:05:32 AM
    Flags                    :  name_canonicalize, pre_authent, renewable, forwardable
    KeyType                  :  aes256_cts_hmac_sha1
    Base64(key)              :  6FT8ompgb7esByuWTc9LDHLtKEhCvkqRY1ayaYzIz+s=
    Base64EncodedTicket   :

      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


    ServiceName              :  MSSQLSvc/SRV22.OSCP.EXAM
    ServiceRealm             :  OSCP.EXAM
    UserName                 :  WS26$
    UserRealm                :  OSCP.EXAM
    StartTime                :  11/26/2026 6:28:47 AM
    EndTime                  :  11/26/2026 11:05:32 AM
    RenewTill                :  12/3/2026 1:05:32 AM
    Flags                    :  name_canonicalize, pre_authent, renewable, forwardable
    KeyType                  :  aes256_cts_hmac_sha1
    Base64(key)              :  b+KQNGCB0DqMXH/pPZweX48vPTlmEE5JPlMYba6sAVw=
    Base64EncodedTicket   :

      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

MariaDB []> show databases;
+--------------------+
| Database           |
+--------------------+
| information_schema |
| mysql              |
| offsecnic_db       |
| performance_schema |
| phpmyadmin         |
| test               |
+--------------------+
6 rows in set (0.250 sec)

MariaDB []> use phpmyadmin;
Reading table information for completion of table and column names
You can turn off this feature to get a quicker startup with -A

Database changed
MariaDB [phpmyadmin]> show tables;
+------------------------+
| Tables_in_phpmyadmin   |
+------------------------+
| pma__bookmark          |
| pma__central_columns   |
| pma__column_info       |
| pma__designer_settings |
| pma__export_templates  |
| pma__favorite          |
| pma__history           |
| pma__navigationhiding  |
| pma__pdf_pages         |
| pma__recent            |
| pma__relation          |
| pma__savedsearches     |
| pma__table_coords      |
| pma__table_info        |
| pma__table_uiprefs     |
| pma__tracking          |
| pma__userconfig        |
| pma__usergroups        |
| pma__users             |
+------------------------+
19 rows in set (0.253 sec)

MariaDB [phpmyadmin]> SHOW columns from pma_users;
ERROR 1146 (42S02): Table 'phpmyadmin.pma_users' doesn't exist
MariaDB [phpmyadmin]> SHOW columns from 'pma_users';
ERROR 1064 (42000): You have an error in your SQL syntax; check the manual that corresponds to your MariaDB server version for the right syntax to use near ''pma_users'' at line 1
MariaDB [phpmyadmin]> SHOW columns from pma__users;
+-----------+-------------+------+-----+---------+-------+
| Field     | Type        | Null | Key | Default | Extra |
+-----------+-------------+------+-----+---------+-------+
| username  | varchar(64) | NO   | PRI | NULL    |       |
| usergroup | varchar(64) | NO   | PRI | NULL    |       |
+-----------+-------------+------+-----+---------+-------+
2 rows in set (0.252 sec)

MariaDB [phpmyadmin]> SHOW columns from pma__userconfig;
+-------------+-------------+------+-----+---------------------+-------------------------------+
| Field       | Type        | Null | Key | Default             | Extra                         |
+-------------+-------------+------+-----+---------------------+-------------------------------+
| username    | varchar(64) | NO   | PRI | NULL                |                               |
| timevalue   | timestamp   | NO   |     | current_timestamp() | on update current_timestamp() |
| config_data | text        | NO   |     | NULL                |                               |
+-------------+-------------+------+-----+---------------------+-------------------------------+
3 rows in set (0.250 sec)

MariaDB [phpmyadmin]> show databases;
+--------------------+
| Database           |
+--------------------+
| information_schema |
| mysql              |
| offsecnic_db       |
| performance_schema |
| phpmyadmin         |
| test               |
+--------------------+
6 rows in set (0.251 sec)

MariaDB [phpmyadmin]> use test;
Database changed
MariaDB [test]> show columns from test;
ERROR 1146 (42S02): Table 'test.test' doesn't exist
MariaDB [test]> show tables;
Empty set (0.248 sec)

MariaDB [test]> use offsecnic_db
Reading table information for completion of table and column names
You can turn off this feature to get a quicker startup with -A

Database changed
MariaDB [offsecnic_db]> use offsecnic_db;
Database changed
MariaDB [offsecnic_db]> show tables;
+------------------------+
| Tables_in_offsecnic_db |
+------------------------+
| smtp_settings          |
| users                  |
+------------------------+
2 rows in set (0.255 sec)

MariaDB [offsecnic_db]> show columns from users;
+------------+--------------+------+-----+---------+----------------+
| Field      | Type         | Null | Key | Default | Extra          |
+------------+--------------+------+-----+---------+----------------+
| id         | int(11)      | NO   | PRI | NULL    | auto_increment |
| email      | varchar(255) | NO   | UNI | NULL    |                |
| password   | varchar(255) | NO   |     | NULL    |                |
| first_name | varchar(100) | NO   |     | NULL    |                |
+------------+--------------+------+-----+---------+----------------+
4 rows in set (0.253 sec)

MariaDB [offsecnic_db]> select * from users;
+----+---------------------+--------------------------------------------------------------+------------+
| id | email               | password                                                     | first_name |
+----+---------------------+--------------------------------------------------------------+------------+
|  1 | o.soaw@oscp.exam    | $2y$10$abcdefghijklmnopqrstuvABCDE1234567890abcdEFGHijklmnoP | Oscar      |
|  2 | j.smith@oscp.exam   | $2y$10$ZyxwvutsrqponmlkjihgFE9876543210zyxwVUTSRqponMLKjihgf | Jasper     |
|  3 | d.arnault@oscp.exam | $2y$10$MnopQRStuvWXYZabcd1234EFGHijkl5678MNOPqrstUVwxYZabCde | David      |
|  4 | p.follo@oscp.exam   | $2y$10$r4Nd0mSaltStr1ngForBcryptHashValueABCDEfghijkLMNOPqrs | Pablo      |
+----+---------------------+--------------------------------------------------------------+------------+
4 rows in set (0.580 sec)

MariaDB [offsecnic_db]> select * from smtp_settings;
+----+----------------+------+-------------------+----------------------------+------------+-------------------+----------------------+-----------+---------------------+---------------------+
| id | host           | port | username          | password                   | encryption | from_email        | from_name            | is_active | created_at          | updated_at          |
+----+----------------+------+-------------------+----------------------------+------------+-------------------+----------------------+-----------+---------------------+---------------------+
|  1 | smtp.oscp.exam |  587 | l.perry@oscp.exam | CredentialShieldDiamond559 | tls        | noreply@oscp.exam | Offsec Notifications |         1 | 2026-02-16 12:31:06 | 2026-02-16 12:31:06 |
+----+----------------+------+-------------------+----------------------------+------------+-------------------+----------------------+-----------+---------------------+---------------------+
1 row in set (0.251 sec)

MariaDB [offsecnic_db]> ^C
MariaDB [offsecnic_db]> use mysql;
Reading table information for completion of table and column names
You can turn off this feature to get a quicker startup with -A

show tables;
Database changed
MariaDB [mysql]> show tables;
+---------------------------+
| Tables_in_mysql           |
+---------------------------+
| column_stats              |
| columns_priv              |
| db                        |
| event                     |
| func                      |
| general_log               |
| global_priv               |
| gtid_slave_pos            |
| help_category             |
| help_keyword              |
| help_relation             |
| help_topic                |
| index_stats               |
| innodb_index_stats        |
| innodb_table_stats        |
| plugin                    |
| proc                      |
| procs_priv                |
| proxies_priv              |
| roles_mapping             |
| servers                   |
| slow_log                  |
| table_stats               |
| tables_priv               |
| time_zone                 |
| time_zone_leap_second     |
| time_zone_name            |
| time_zone_transition      |
| time_zone_transition_type |
| transaction_registry      |
| user                      |
+---------------------------+
31 rows in set (0.248 sec)

MariaDB [mysql]> show columns from user;
+------------------------+---------------------+------+-----+----------+-------+
| Field                  | Type                | Null | Key | Default  | Extra |
+------------------------+---------------------+------+-----+----------+-------+
| Host                   | char(60)            | NO   |     |          |       |
| User                   | char(80)            | NO   |     |          |       |
| Password               | longtext            | YES  |     | NULL     |       |
| Select_priv            | varchar(1)          | YES  |     | NULL     |       |
| Insert_priv            | varchar(1)          | YES  |     | NULL     |       |
| Update_priv            | varchar(1)          | YES  |     | NULL     |       |
| Delete_priv            | varchar(1)          | YES  |     | NULL     |       |
| Create_priv            | varchar(1)          | YES  |     | NULL     |       |
| Drop_priv              | varchar(1)          | YES  |     | NULL     |       |
| Reload_priv            | varchar(1)          | YES  |     | NULL     |       |
| Shutdown_priv          | varchar(1)          | YES  |     | NULL     |       |
| Process_priv           | varchar(1)          | YES  |     | NULL     |       |
| File_priv              | varchar(1)          | YES  |     | NULL     |       |
| Grant_priv             | varchar(1)          | YES  |     | NULL     |       |
| References_priv        | varchar(1)          | YES  |     | NULL     |       |
| Index_priv             | varchar(1)          | YES  |     | NULL     |       |
| Alter_priv             | varchar(1)          | YES  |     | NULL     |       |
| Show_db_priv           | varchar(1)          | YES  |     | NULL     |       |
| Super_priv             | varchar(1)          | YES  |     | NULL     |       |
| Create_tmp_table_priv  | varchar(1)          | YES  |     | NULL     |       |
| Lock_tables_priv       | varchar(1)          | YES  |     | NULL     |       |
| Execute_priv           | varchar(1)          | YES  |     | NULL     |       |
| Repl_slave_priv        | varchar(1)          | YES  |     | NULL     |       |
| Repl_client_priv       | varchar(1)          | YES  |     | NULL     |       |
| Create_view_priv       | varchar(1)          | YES  |     | NULL     |       |
| Show_view_priv         | varchar(1)          | YES  |     | NULL     |       |
| Create_routine_priv    | varchar(1)          | YES  |     | NULL     |       |
| Alter_routine_priv     | varchar(1)          | YES  |     | NULL     |       |
| Create_user_priv       | varchar(1)          | YES  |     | NULL     |       |
| Event_priv             | varchar(1)          | YES  |     | NULL     |       |
| Trigger_priv           | varchar(1)          | YES  |     | NULL     |       |
| Create_tablespace_priv | varchar(1)          | YES  |     | NULL     |       |
| Delete_history_priv    | varchar(1)          | YES  |     | NULL     |       |
| ssl_type               | varchar(9)          | YES  |     | NULL     |       |
| ssl_cipher             | longtext            | NO   |     |          |       |
| x509_issuer            | longtext            | NO   |     |          |       |
| x509_subject           | longtext            | NO   |     |          |       |
| max_questions          | bigint(20) unsigned | NO   |     | 0        |       |
| max_updates            | bigint(20) unsigned | NO   |     | 0        |       |
| max_connections        | bigint(20) unsigned | NO   |     | 0        |       |
| max_user_connections   | bigint(21)          | NO   |     | 0        |       |
| plugin                 | longtext            | NO   |     |          |       |
| authentication_string  | longtext            | NO   |     |          |       |
| password_expired       | varchar(1)          | NO   |     |          |       |
| is_role                | varchar(1)          | YES  |     | NULL     |       |
| default_role           | longtext            | NO   |     |          |       |
| max_statement_time     | decimal(12,6)       | NO   |     | 0.000000 |       |
+------------------------+---------------------+------+-----+----------+-------+
47 rows in set (0.252 sec)

MariaDB [mysql]> select User, Password, password_expired from users;
ERROR 1146 (42S02): Table 'mysql.users' doesn't exist
MariaDB [mysql]> select User, Password, password_expired from user;
+----------------+-------------------------------------------+------------------+
| User           | Password                                  | password_expired |
+----------------+-------------------------------------------+------------------+
| root           |                                           | N                |
| offsecnic_user | *96886EC85CCBBED6ED7938C33D55A8D4C846790D | N                |
| root           |                                           | N                |
| root           |                                           | N                |
| pma            |                                           | N                |
+----------------+-------------------------------------------+------------------+
5 rows in set (0.248 sec)

MariaDB [mysql]> 



---
## Interesting Files/Paths

```
+---Administrator
|   +---Contacts
|   +---Desktop
|   |       Microsoft Edge.lnk
|   |       proof.txt
|   |
+---administrator.OSCP
|   +---Documents
|   |   \---WindowsPowerShell
|   |       \---Scripts
|   |           \---InstalledScriptInfos
|   +---Downloads
|   |       DefenderRemover.exe
|   |       WinDefCtl.7z
|   |       WinDefCtl.exe
|   |       WinDefCtl_arm64.exe
|   |       WinRAR-723.exe
+---Public
|   |   Offsec.jpg

```
---
## Attack Ideas

80, 135, 139, 443, 445, 3306, 47001,

Some user names on the 80 443 websites

Test callback using domain search but no answer from nc -lvnp

There are still interesting files to explore on the other users on MS01 as r.andrews

---
## Steps to User.txt

---
## Steps to root.txt

ROOT MS01 at 6:04PM

![[Pasted image 20261126180856.png]]

![[Pasted image 20261126180719.png]]

---

# Steps to PIVOT

Checked mimikatz
Kerberoasting half fail?
checked recyclebin
Nothing interesting in DC SMB share
Enumerated Offsec.jpg with exiftool
Enumerated the scripts folder
Checked ldapsearch

cmdkey /list nothing



## User Flag

```

```

## Root Flag

```

```