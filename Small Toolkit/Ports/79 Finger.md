### **79 → Finger**

- Service: Finger
- Purpose:
    - Shows logged-in users
    - Can reveal usernames, home dirs, shells
-
```dataviewjs
const page = dv.page("Synced OSCP Notes/Top/Active Notes");const ip = page?.IP ?? "NO IP FOUND";

const command = `finger @${ip}`;

dv.paragraph("```bash\n" + command + "\n```");
```
https://pentestmonkey.net/tools/user-enumeration/finger-user-enum

finger-user-enum v1.0

```
wget https://pentestmonkey.net/tools/finger-user-enum/finger-user-enum-1.0.tar.gz
```

```
tar -xf finger-user-enum-1.0.tar.gz
```

```
cd finger-user-enum=1.0
```


---

USAGE : 
```dataviewjs
const page = dv.page("Synced OSCP Notes/Top/Active Notes");const ip = page?.IP ?? "NO IP FOUND";

const command = `./finger-user-enum.pl -U /usr/share/seclists/Usernames/Names/names.txt -t ${ip}`;

dv.paragraph("```bash\n" + command + "\n```");
```
