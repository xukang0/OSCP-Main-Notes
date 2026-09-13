
[[Current Affairs Notes Template]]

# Steps to User flag

nmap scan shows domain is blackfield.local

Add it to /etc/hosts

53DNS axfr transfer failed

88Kerberos open, run kerbrute and rid lookup for users

managed to get a good list of users from rid lookup

Attempt to as-rep these list of users

1 hit, audit2020 gives kerberos hash

john cracks the hash and we have creds for 'support:#00^BlackKnight'

Run nxc sweep on these creds, as well as test the password against all users

Password doesnt work for any other users

RPCclient fails

SMBClient anonymous listing shows "profiles$"

Enum4linux-ng gives us OS information and domain information. Windows 10, Windows server 2019 and windows server 2016

SMB profiles$ give us a whole bunch of profile names. Added to user1 file

[[Sanitizing Files]] and getting a clean user1 file

asrep roast it + trying support pw on it. None hit.

Try ldap. ldapsearch negative

Running bloodhound-python and ingesting, discover support has force password change over audit2020

Change creds with rpcclient to audit2020:Retric!

