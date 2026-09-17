
[[Current Affairs Notes Template]]

# Steps to User flag

Nmap scan shows domain is administrator.htb. Add to /etc/hosts

Trying olivia creds to login ftp doesnt work

53 DNS dig finds nothing

RID brute using olivia creds yield list of users. Added to list

RPCclient using olivia fails

enum4linux-ng shows me target OS version and FQDN

Nothing interesting from SMB

Using nxc sweep against oliva creds shows win-rm as pwned

EvilwinRM to enter olivia.

Emily is the only other user on the system

Olivia has GenericAll against Michael

Michael has forcechangepassword of Benjamin

Enter Michael first. Michael entered. Use NXC to check his creds. Nothing.

Onto Benjamin Next. Benjamin on nxc-sweep shows he has access to something on FTP

a psafe3 file was found.

Decrypt it with john for master password, start pwsafe software and open password database

Copy emily password and try nxc-sweep. It works

Evilwinrm into emily. It fails

Use runas to get into emily. Success

User flag on emily desktop

Emily is local administrator but not domain administrator

Emily has genericwrite over ethan

Ethan has GetC GetChangesAll dSet over domain














