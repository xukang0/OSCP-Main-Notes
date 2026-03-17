# ⚡ Basic Usage

## Search for exploits

searchsploit apache 2.4.10  
searchsploit openssh 6.7  
searchsploit unrealircd

## Show full path to exploit

searchsploit -p unrealircd

---

## Copy exploit to your working directory

searchsploit -m exploits/unix/irc/16922.c

Then:

gcc 16922.c -o exploit

---

## Update database

searchsploit -u