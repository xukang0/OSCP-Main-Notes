To generate a key pair

```
ssh-keygen -t ed25519 -f ~/.ssh/id_ed25519
```

Your SSH public key is normally stored in `~/.ssh/` and has a `.pub` extension.

```
echo MYPUBKEY > /root/.ssh/authorized_keys
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
