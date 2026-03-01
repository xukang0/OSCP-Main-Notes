`find` 
	(locate a file or directory),
	Example : find / -name flag.txt 2>/dev/null
	sudo find /usr/share/ -name "namelist.txt"

```
find / -name flag.txt 2>/dev/null
```
### 🧠 What `find / -name Responder.conf` means:

- `find` is a command-line tool to **search for files and directories**.
    
- `/` tells it to **start the search at the root of the filesystem** — basically, search **everywhere**.
    
- `-name Responder.conf` tells `find` to **look for a file with that exact name**.

`pwd` 
	print working directory 

`cd` 
	change directory 

`ls` 
	list file or directory contents 

ls -la (list file, showing longer format)

touch
	create file

`mkdir` (make directory), 

`rmdir` (remove directory),

`rm` (remove)

`cp` (copy)
	cp note1 note2

`mv` (move)
	mv note2 note3

`cat` (concatenate or read file), 

`less`/`more` (show files a page at a time), 

`editor` (start a text editor), 

## 🧠 What `ss -tln` Actually Does

ss (socket statistics)

| Option | Meaning                                                        |
| ------ | -------------------------------------------------------------- |
| `-t`   | Show only **TCP** connections (not UDP)                        |
| `-l`   | Show only **listening** sockets                                |
| `-n`   | Show **numeric ports/IPs** (no DNS or service name resolution) |

```
ss -tln
```

![[Pasted image 20250520020259.png]]

Running without -n flag shows the service name instead of port no.

```
ss -tl
```

![[Pasted image 20250520020420.png]]
## Next

whereis 
	locates programs
	Example : whereis (python)

grep (finds words in a file)
	Example : grep THM dictionary.txt (Find "THM" in the file "dictionary.txt")

apropos 
	help find cmds with keywords
	Example : apropos (search)

`free` (display memory information), 

`df` (show disk free space), 

`id` (display the identity of the user along with the list of groups they belong to), 

`dmesg` (review kernel logs), and 

`journalctl` (show all available logs).

You can inspect the hardware on a Kali system with several commands: 

`lspci` (list PCI devices), 

`lsusb` (list USB devices), and 

`lspcmcia` lists PCMCIA cards.

 A process is a running instance of a program, which requires memory to store both the program itself and its operating data. 

You can manage processes with commands like: 

`ps` (show processes),
	ps aux (show processes and associated users)

`kill` (kill processes), 

`bg` (send process to background), 

`fg` (bring background process to foreground), and 

`jobs` (show background processes).

Unix-like systems are multi-user. They support multiple users and groups and allow control over actions, based on permissions.  

You can manage file and directory rights with several commands, including: 

`chmod` (change permissions), `chown` (change owner), and `chgrp` (change group)


Installing Packages with APT

```
# apt install kali-tools-gpu
```

To upgrade, use `apt update` followed by either `apt upgrade`, `apt-get upgrade`, or `aptitude safe-upgrade`.