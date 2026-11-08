
[[Current Affairs Notes Template]]

# Steps to User flag

Running Machine 2 creds using nxc sweep, creds pwned for winrm, ssh, smb shares, 

Use creds for RID brute for a list of users as well (MS01:users1)

Evil win-rm into Eric.Willows. There are a few user accounts inside

Found mysql on ms01.oscp.exam. Error message says this hostname not allowed to connect

Interesting stuff in C:\setup, but ultimately led nowhere

oscp\eric.wallows has SeImpersonatePriv

Enumeration shows machine is windows 10 pro.

SharpEfsPotato works. NT authority/system. Part of Administrators group

Enumerated every single Desktop and Documents of Users

LaZagne gives some hashes

Administrator:500:aad3b435b51404eeaad3b435b51404ee:3c4495bbd678fac8c9d218be4f2bbc7b:::
Guest:501:aad3b435b51404eeaad3b435b51404ee:31d6cfe0d16ae931b73c59d7e0c089c0:::
DefaultAccount:503:aad3b435b51404eeaad3b435b51404ee:31d6cfe0d16ae931b73c59d7e0c089c0:::
WDAGUtilityAccount:504:aad3b435b51404eeaad3b435b51404ee:11ba4cb6993d434d8dbba9ba45fd9011:::
Mary.Williams:1002:aad3b435b51404eeaad3b435b51404ee:9a3121977ee93af56ebd0ef4f527a35e:::
support:1003:aad3b435b51404eeaad3b435b51404ee:d9358122015c5b159574a88b3c0d2071:::
cloudbase-init:1004:aad3b435b51404eeaad3b435b51404ee:cb47daeda02df568b81ca633a210a76a:::
Admin:1005:aad3b435b51404eeaad3b435b51404ee:bd063c2d424044053dadc6a197c8e222:::

Useless.

Use ligolo to reach internal subnet of MS02.

Try nxc-sweep of celia.almeda hash against MS02. Works. 

Nxc shows winrm Pwned. Enter celia almeda



