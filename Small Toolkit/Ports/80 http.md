* Check version using `searchsploit` for public exploits (Traversal, SQLi, RCE)
* Check to see if anything else is running using `whatweb http://10.10.10.10` (searchsploit, wordpress)
* Fully enumerate with directory brute-forcing
	* Run multiple tools and check for file extensions, try from deeper directories
* Visit site in the browser and look for any context clues
	* See if there's any hint for FQDN and put it in `/etc/hosts`
	* See if there's any hints to valid users or software in pages or source code
* Test everything for default credentials or username being the password

Enumerate directories using GoBuster
[[Gobuster Directory Enumeration Dir Enum]]
```dataviewjs
const page = dv.page("Templater/IP");const ip = page?.IP ?? "NO IP FOUND";

const command = `gobuster dir --url http://${ip}/ --wordlist /usr/share/wordlists/dirb/big.txt`;

dv.paragraph("```bash\n" + command + "\n```");
```
