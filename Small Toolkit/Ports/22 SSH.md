- `id_rsa` is the private key that should be kept secret and never shared
    
- `id_rsa.pub` is the public key that can be shared with other systems

These keys work together like a lock and key. The public key (`id_rsa.pub`) is installed on remote machines you want to connect to, while the private key (`id_rsa`) on your local machine proves your identity. Now, let’s download the private key and exit the FTP connection.
```dataviewjs
const page = dv.page("Synced OSCP Notes/Top/Active Notes");const ip = page?.IP ?? "NO IP FOUND";

const command = `ssh [USER]@${ip} -p [portno]`;

dv.paragraph("```bash\n" + command + "\n```");
```
```
chmod 600 id_rsa
```
```dataviewjs
const page = dv.page("Synced OSCP Notes/Top/Active Notes");const ip = page?.IP ?? "NO IP FOUND";

const command = `ssh -i id_rsa [user]@${ip}`;

dv.paragraph("```bash\n" + command + "\n```");
```

ssh jan@10.10.35.240

ssh jan@10.10.35.240 2121 

copy id_rsa and login SSH and

---

port forward our connection to the remote host's internal port
```dataviewjs
const page = dv.page("Synced OSCP Notes/Top/Active Notes");const ip = page?.IP ?? "NO IP FOUND";

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