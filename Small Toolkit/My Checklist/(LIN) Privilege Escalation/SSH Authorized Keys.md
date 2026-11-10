To generate a key pair

id_rsa
```
ssh-keygen -t rsa -b 4096 -f ~/.ssh/id_rsa
```

id_ed25519
```
ssh-keygen -t ed25519 -f ~/.ssh/id_ed25519
```

Your SSH public key is normally stored in `~/.ssh/` and has a `.pub` extension.

id_ed25519.pub or id_rsa.pub

```
echo MYPUBKEY > /home/[user]/.ssh/authorized_keys
```

Once your public key has been successfully added to the target's `/root/.ssh/authorized_keys`, you connect using the matching private key from your Kali machine.

For example, if your key pair is `id_rsa`:
```dataviewjs
const page = dv.page("Synced OSCP Notes/Top/Active Machine");const ip = page?.IP ?? "NO IP FOUND";

const command = `ssh -i ~/.ssh/id_rsa root@${ip}`;

dv.paragraph("```bash\n" + command + "\n```");
```
If you're using Ed25519
```dataviewjs
const page = dv.page("Synced OSCP Notes/Top/Active Machine");const ip = page?.IP ?? "NO IP FOUND";

const command = `ssh -i ~/.ssh/id_ed25519 root@${ip}`;

dv.paragraph("```bash\n" + command + "\n```");
```

---

### Fix it

If you're certain `192.168.162.150` is still your intended lab target, run:
```dataviewjs
const page = dv.page("Synced OSCP Notes/Top/Active Machine");const ip = page?.IP ?? "NO IP FOUND";

const command = `ssh-keygen -f ~/.ssh/known_hosts -R ${ip}`;

dv.paragraph("```bash\n" + command + "\n```");
```

This removes the old host key entry for that IP.

Then reconnect:

```
ssh -i ~/.ssh/id_rsa dev@192.168.162.150
```