
[[Current Affairs Notes Template]]

# Steps to User flag

nmap scan shows domain is puppy.htb

53 DNS dig nothing

111 rpcbind nothing

135 RPCclient nothing

139 SMBmap only default shares. There is a dev share that i have no access to

enum4linux-ng tells us OS version and domain information

RID brute gives me a list of users

As-rep this list gives nothing

levi.james is a member of HR group which has genericwrite over dev group

Maybe if we enter dev group we can read the dev share

GenericWrite > add levi.james as a member of Dev group allows me to read the dev share

Use keepass2john to crack recovery.kdbx file for "liverpool" password














