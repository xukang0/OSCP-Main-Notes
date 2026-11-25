These devices store LDAP and SMB credentials, in order for the printer to query the user list from Active Directory, and to be able to save scanned files to a user drive. These configuration pages typically allow the domain controller or file server to be specified. Let's stand up a listener on port 389 (LDAP) and specify our tun0 IP address in the Server address field.

Try to ping yourself with a listener opener, the printer might try to authenticate back to listener using the password accidentally

```
sudo nc -lvnp 389
```

---
# dump domain information from ldap  
```dataviewjs
const page = dv.page("Synced OSCP Notes/Top/Active Machine");const ip = page?.IP ?? "NO IP FOUND";

const command = `ldapdomaindump -u '[$domain]\[$user]' -p [PW] ${ip}`;

dv.paragraph("```bash\n" + command + "\n```");
```
# jq query to parse usernames/descriptions  

```
cat domain_users.json | jq '.[].attributes | {sAMAccountName, description}'
```

---

```dataviewjs
const page = dv.page("Synced OSCP Notes/Top/Active Machine");const ip = page?.IP ?? "NO IP FOUND";

const command = `ldapsearch -H ldap://${ip} -x -s base namingcontexts`;

dv.paragraph("```bash\n" + command + "\n```");
```
```dataviewjs
const page = dv.page("Synced OSCP Notes/Top/Active Machine");const ip = page?.IP ?? "NO IP FOUND";

const command = `ldapsearch -v -x -b "DC=hutch,DC=offsec" -H "ldap://${ip}" > ldapsearchoutput.txt`;

dv.paragraph("```bash\n" + command + "\n```");
```
Authenticated ldapsearch
```dataviewjs
const page = dv.page("Synced OSCP Notes/Top/Active Machine");

const KaliIP = page?.["KALI IP"] ?? "NO KALI IP FOUND";
const IP = page?.IP ?? "NO IP FOUND";const discoveredDomain = page?.["Discovered Web Domain"] ?? "NO DOMAIN FOUND";

const command = `ldapsearch -x -H 'ldap://$(IP)' -D ‘hutch\(USER)’ -w ‘(PW)’ -b 'dc=hutch,dc=offsec'`;

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

389/tcp   open  ldap          Microsoft Windows Active Directory LDAP (Domain: hutch.offsec, Site: Default-First-Site-Name)

![[Pasted image 20260910101647.png]]

Example : Can ping back own kali attacker port 389 where nc is listening to catch an accidental password

![[Pasted image 20260910101736.png]]