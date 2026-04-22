Basic Usage
```dataviewjs
const page = dv.page("Synced OSCP Notes/Top/Active Notes");
const discoveredDomain = page?.["Discovered Web Domain"] ?? "NO DOMAIN FOUND";

const command = `wpscan --url http://${discoveredDomain}`;

dv.paragraph("```bash\n" + command + "\n```");
```
Scan all (Users,Plugins, Themes)
```dataviewjs
const page = dv.page("Synced OSCP Notes/Top/Active Notes");
const discoveredDomain = page?.["Discovered Web Domain"] ?? "NO DOMAIN FOUND";

const command = `wpscan --url http://${discoveredDomain} -e`;

dv.paragraph("```bash\n" + command + "\n```");
```
Precise scan
```dataviewjs
const page = dv.page("Synced OSCP Notes/Top/Active Notes");
const discoveredDomain = page?.["Discovered Web Domain"] ?? "NO DOMAIN FOUND";

const command = `wpscan --url http://${discoveredDomain} -e u,p,t`;

dv.paragraph("```bash\n" + command + "\n```");
```
Last resort
```dataviewjs
const page = dv.page("Synced OSCP Notes/Top/Active Notes");
const discoveredDomain = page?.["Discovered Web Domain"] ?? "NO DOMAIN FOUND";

const command = `wpscan --url http://${discoveredDomain} -e --plugins-detection mixed --force`;

dv.paragraph("```bash\n" + command + "\n```");
```
- `u` = users
- `p` = plugins
- `t` = themes

Password Brute Force (User List, Password List)

```dataviewjs
const page = dv.page("Synced OSCP Notes/Top/Active Notes");
const discoveredDomain = page?.["Discovered Web Domain"] ?? "NO DOMAIN FOUND";

const command = `wpscan --url http://${discoveredDomain} -U users.txt -P passwords.txt`;

dv.paragraph("```bash\n" + command + "\n```");
```
Wordlist
```dataviewjs
const page = dv.page("Synced OSCP Notes/Top/Active Notes");
const discoveredDomain = page?.["Discovered Web Domain"] ?? "NO DOMAIN FOUND";

const command = `wpscan --url http://${discoveredDomain} -U admin -P /usr/share/wordlists/rockyou.txt`;

dv.paragraph("```bash\n" + command + "\n```");
```

URL to get to themes code execution
```dataviewjs
const page = dv.page("Synced OSCP Notes/Top/Active Notes");
const discoveredDomain = page?.["Discovered Web Domain"] ?? "NO DOMAIN FOUND";

const command = `http://${discoveredDomain}/wp-content/themes/twentyfifteen/404.php`;

dv.paragraph("```bash\n" + command + "\n```");
```
