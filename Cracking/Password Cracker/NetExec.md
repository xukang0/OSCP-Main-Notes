
{nfs,ftp,ssh,winrm,smb,wmi,rdp,mssql,ldap,vnc}
```dataviewjs
const page = dv.page("Templater/IP");const ip = page?.IP ?? "NO IP FOUND";

const command = `netexec <service> ${ip} -u [userlist] -p [pwlist]`;

dv.paragraph("```bash\n" + command + "\n```");
```
```dataviewjs
const page = dv.page("Synced OSCP Notes/Top/Active Machine");const ip = page?.IP ?? "NO IP FOUND";

const command = `netexec winrm ${ip} -u user.list -p password.list`;

dv.paragraph("```bash\n" + command + "\n```");
```


Use the username and password to shell login to windows using [[Tools/Evil-Winrm|Evil-Winrm]]

```dataviewjs
const page = dv.page("Templater/IP");const ip = page?.IP ?? "NO IP FOUND";

const command = `netexec smb ${ip} -u "user" -p "password" --shares`;

dv.paragraph("```bash\n" + command + "\n```");
```
