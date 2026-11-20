
[[Current Affairs Notes Template]]

# Steps to Aero
### User flag

Dirbust port 80, 81, and 443 found api/heartbeat

Mention of aerospike

Exploit db found poc get RCE

Flag on aero /home dir

### Root flag

use [[Screen Priv Esc]]

Flag on root desktop

---
# Steps to Crystal
### User flag

Ports 21,22 and 80 open

nmap tells us git repository found

[[GIT dumper]]

view previous commits and find 

stuart@challenge.lab
BreakingBad92

dean@challenge.pwk
BreakingBad92

Can access stuart ssh and ftp. His FTP mirrors his SSH

there is sitebackup3

zip2john and 7z

configuration.php shows 

$user = 'joomla';
	public $password = 'Password@1';
	public $secret = 'Ee24zIK4cDhJHL4H';
This secret password works for su chloe

enumerate chloe

chloe can sudo -i

sudo -i for root

### Root flag



---
# Steps to Hermes
### User flag



### Root flag






