
[[Current Affairs Notes Template]]

# Steps to User flag

nmap scan shows me domain name and  DNS_Computer_Name: ResourceDC.resourced.local

resourced.local add to /etc/hosts

port 53 : Dig axfr failed
port 88 : rid brute shows nothing. 
kerbrute shows administrator
port 139 : enum4linux finds a list of users and their roles

In the Desc contains his creds

V.Ventz	Name: (null)	Desc: New-hired, reminder: HotelCalifornia194!

nxc sweep : 

smb
rdp
ldap

Test other users using same password : Nothing

Check SMB contents

There is ntdsdit and system and security

use impacket to secretsdump this

get nthashes

nxc sweep to see which hash is still valid

 [+] resourced.local\L.Livingstone:19a3a7550ce8c505c2d46b5e39d6f808 

evilwin-rm to enter. L.Livingstone Desktop contains local.txt

Using bloodhound, L.Livingstone has genericall over resourcedc.resourced.local. This one has DCSync to resourced.local

Follow genericall > [[RBCD]] to pivot into resourcedc.resouced.local to gain root shell

proof.txt in administrator desktop







Note that evil win-rm and rdp are available
