## Root Commands

Run an interactive login shell as root
```
sudo -i
```

Superuser Do switch user into Root account
```
sudo su root
```

/bin/bash root
```
/bin/bash -p
```

Append ALL permissions into sudoers file
```
echo [user] ALL=(ALL) ALL >> /etc/sudoers
```

---
## Reading root's id_rsa

```
cat /root/.ssh/id_rsa
```

On KALI ATTACKER, Paste the SSH Key
```
gedit id_rsa
```

Login as root
```dataviewjs
const page = dv.page("Synced OSCP Notes/Top/Active Machine");const ip = page?.IP ?? "NO IP FOUND";

const command = `chmod 600 id_rsa && ssh root@${ip} -i id_rsa`;

dv.paragraph("```bash\n" + command + "\n```");
```

---