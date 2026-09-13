
[[Current Affairs Notes Template]]]

# Steps to User flag

Nmap scan shows clock skew and domain name frizz.htb

Test DNS. Nothing.

Test RPC. Nothing.

Test SMB. Enum4linux-ng says there is no server. Im guessing this is a pivot internal server

Test Kerb. Cannor rid lookup. Nothing

Visit webpage

Page redirects me to frizzdc.frizz.htb so i add to /etc/hosts

On the page, users mentioned are Mike Smith, Fiona Frizzle, and there is a mention of Azure AD. There is php files

Webpage powered by Gibbon v25.0.00

Attempted various path traversal methods all failed

Tried putting Mike Smith and Fiona Frizzle into users and creating various combinations of possible usernames, kerbrute shows F.Frizzle exists.

F.Frizzle :
1. cant be asrep roasted
2. doesnt use same password as username
GibbonLMS has a github page. I realized i can use path traversal to read existing files

https://github.com/ulricvbs/gibbonlms-filewrite_rce

There is a Gibbon CVE unauthenticated RCE for v 25.01 and before.

It works out of the box and i get a webshell.

Try php payload for Rev shell

I try to upload shell.php through webshell and access through traversal. Pentestmonkey doesnt work so try nc64

running systeminfo through webshell tells us this is windows 2022 and x64

works and i am in frizz\w.webservice

inetpub in root folder. ASPX potential.

nothing in autologon

On Gibbon-LMS there is a config.php file with database creds

in C:\xampp\mysql\bin\sql.exe can execute mysql

