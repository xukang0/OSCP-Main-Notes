Identify the likely web root

On Debian-based Linux systems, Apache commonly uses:
```dataviewjs
const page = dv.page("Synced OSCP Notes/Top/Active Machine");

const KaliIP = page?.["KALI IP"] ?? "NO KALI IP FOUND";
const IP = page?.IP ?? "NO IP FOUND";const discoveredDomain = page?.["Discovered Web Domain"] ?? "NO DOMAIN FOUND";

const command = `/var/www/html/`;

const button = dv.container.createEl("button", {
    text: command
});

button.style.cssText = `
    font-family: monospace;
    font-size: 0.85em;
    padding: 2px 6px;
    border: 1px solid var(--background-modifier-border);
    border-radius: 4px;
    background: var(--code-background);
    color: var(--text-normal);
    cursor: pointer;
`;

button.addEventListener("click", async () => {
    try {
        await navigator.clipboard.writeText(command);
        button.textContent = "Copied!";
        setTimeout(() => button.textContent = command, 250);
    } catch {
        button.textContent = "Copy failed";
    }
});
```

[[0000006|Visit site]]
```dataviewjs
const page = dv.page("Synced OSCP Notes/Top/Active Machine");

const KaliIP = page?.["KALI IP"] ?? "NO KALI IP FOUND";
const IP = page?.IP ?? "NO IP FOUND";const discoveredDomain = page?.["Discovered Web Domain"] ?? "NO DOMAIN FOUND";

const command = `http://${discoveredDomain}/`;

const button = dv.container.createEl("button", {
    text: command
});

button.style.cssText = `
    font-family: monospace;
    font-size: 0.85em;
    padding: 2px 6px;
    border: 1px solid var(--background-modifier-border);
    border-radius: 4px;
    background: var(--code-background);
    color: var(--text-normal);
    cursor: pointer;
`;

button.addEventListener("click", async () => {
    try {
        await navigator.clipboard.writeText(command);
        button.textContent = "Copied!";
        setTimeout(() => button.textContent = command, 250);
    } catch {
        button.textContent = "Copy failed";
    }
});
```
View source
Identify tech/CMS
[[0000008|whatweb]]
[[0000009|Test parameters (?id=1, ?page=) | ?[parameter]=0]]
Analyze error page
[[Nickel|Curl dead end redirects for error msg]]
[[0000010|Curl -i domain]]

#### Brute Force
[[0000011|Feroxbuster Directories brute force (medium)]]
/usr/share/seclists/Discovery/Web-Content/raft-medium-directories.txt
[[0000011|Feroxbuster WebList brute force]]
[[0000012|Vhost brute force]]
[[0000013|Feroxbuster File directories sweep]]
[[0000038|Feroxbuster API discovery]]

#### Vulnerability Testing
[[0000014|LFI (../../../../etc/passwd)]]
[[0000015|SQLi (test' or 1=1;-- -) ]] | [[SQL Injection]]
[[Synced OSCP Notes/Tools/SQLmap|SQLmap]]
[[0000016|Command Injection (;whoami)]]
PHP code inclusion
File upload (if available)
[[Hexedit]]

#### Hidden Content
Check JS files
Check comments
Check backups (.bak, .zip)

#### Contingencies

#### Admin Login
Discover software version
Research about software
Search and Try Default credentials
Research CVEs related to version

#### Registration
Register an account
Login using registered account

User Login
Default credentials
creds search [service]

Reset Password (Email)
If invalid email = does not match our records, SQLi (test' or 1=1;-- -)  [[SQL Injection|link]]

#### Admin Dashboards
Search for framework CVEs
Search for dependencies CVEs
File Uploads for PHP arbitrary code execution [[Arbitrary File Upload Vulnerability|link]]

Others
#### .git / git dumper
Run [[GIT dumper]]
Search for creds
Check commit history
#### Hash Found
SSH as is
 [CyberChef](https://cyberchef.org)
 [[Hashcat]]

#### Wordpress Scan
Default creds
[[Wordpress Scan]]


[[Searchsploit]]