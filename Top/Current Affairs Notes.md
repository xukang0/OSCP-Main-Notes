
[[Current Affairs Notes Template]]

---
# Steps to MS01 

### Root flag

Test given creds with nxc

ldapsearch shows domain name is laser.com

eric creds only work with RPC

net rpc user -U 'laser.com/Eric.Wallows%EricLikesRunning800' -S 192.168.245.172 gives a list of domain users. Add to users

For eric.wallows on MS01 there is a writable share called apps

Try to [[SMB NTLMv2 Relay]]

hash captured

Administrator:500:aad3b435b51404eeaad3b435b51404ee:15759746f66f2da88d58f0160f8ee676:::
Admin:1001:aad3b435b51404eeaad3b435b51404ee:3d560aa3cba6bb673b7ef3a30628bf16:::

use psexec to enter NT authority of .174

Flag on administrator desktop

### Pivoting

There is a pcapng file on Administrator documents. With wireshark, fine Yulia.weber:Laser777


---

# Steps to MS02 

### User flag




### Root flag



### Pivoting


# Steps to DC01

### User flag



### Root flag



### Pivoting



---

# Steps to Frankfurt
### User flag



### Root flag

---
# Steps to Charlie
### User flag



### Root flag



---
# Steps to Pascha
### User flag



### Root flag






