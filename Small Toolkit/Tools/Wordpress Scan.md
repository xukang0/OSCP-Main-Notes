Register: [https://wpscan.com](https://wpscan.com)
```dataviewjs
const page = dv.page("Synced OSCP Notes/Top/Active Notes");
const discoveredDomain = page?.["Discovered Web Domain"] ?? "NO DOMAIN FOUND";

const command = `wpscan --url http://${discoveredDomain} --api-token YOUR_TOKEN`;

dv.paragraph("```bash\n" + command + "\n```");
```
Basic Usage
```dataviewjs
const page = dv.page("Synced OSCP Notes/Top/Active Notes");
const discoveredDomain = page?.["Discovered Web Domain"] ?? "NO DOMAIN FOUND";

const command = `wpscan --url http://${discoveredDomain} --api-token YOUR_TOKEN`;

dv.paragraph("```bash\n" + command + "\n```");
```
Scan all (Users,Plugins, Themes)
```dataviewjs
const page = dv.page("Synced OSCP Notes/Top/Active Notes");
const discoveredDomain = page?.["Discovered Web Domain"] ?? "NO DOMAIN FOUND";

const command = `wpscan --url http://${discoveredDomain} -e --api-token YOUR_TOKEN`;

dv.paragraph("```bash\n" + command + "\n```");
```
Precise scan
```dataviewjs
const page = dv.page("Synced OSCP Notes/Top/Active Notes");
const discoveredDomain = page?.["Discovered Web Domain"] ?? "NO DOMAIN FOUND";

const command = `wpscan --url http://${discoveredDomain} -e u,p,t --api-token YOUR_TOKEN`;

dv.paragraph("```bash\n" + command + "\n```");
```
- `u` = users
- `p` = plugins
- `t` = themes

Password Brute Force (User List, Password List)

```dataviewjs
const page = dv.page("Synced OSCP Notes/Top/Active Notes");
const discoveredDomain = page?.["Discovered Web Domain"] ?? "NO DOMAIN FOUND";

const command = `wpscan --url http://${discoveredDomain} -U users.txt -P passwords.txt --api-token YOUR_TOKEN`;

dv.paragraph("```bash\n" + command + "\n```");
```
Wordlist
```dataviewjs
const page = dv.page("Synced OSCP Notes/Top/Active Notes");
const discoveredDomain = page?.["Discovered Web Domain"] ?? "NO DOMAIN FOUND";

const command = `wpscan --url http://${discoveredDomain} -U admin -P /usr/share/wordlists/rockyou.txt --api-token YOUR_TOKEN`;

dv.paragraph("```bash\n" + command + "\n```");
```

