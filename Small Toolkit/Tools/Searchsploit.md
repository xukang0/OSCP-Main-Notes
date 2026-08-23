# ⚡ Basic Usage

## Search for exploits

searchsploit apache 2.4.10  
searchsploit openssh 6.7  
searchsploit unrealircd

## Show full path to exploit

Examine exploit
```
searchsploit -x unrealircd
```

---

## Copy exploit to your working directory

Mirror file
```
searchsploit -m exploits/unix/irc/16922.c
```

---
if c.

Then:

gcc 16922.c -o exploit

---

if rb.

Then : 

```
head exploit.rb
```

- no `class MetasploitModule`
- no `Msf::Exploit`

then it is a normal Ruby script.

Run it with:

ruby exploit.rb

## Update database

searchsploit -u