These devices store LDAP and SMB credentials, in order for the printer to query the user list from Active Directory, and to be able to save scanned files to a user drive. These configuration pages typically allow the domain controller or file server to be specified. Let's stand up a listener on port 389 (LDAP) and specify our tun0 IP address in the Server address field.

```
sudo nc -lvnp 389
```
```dataviewjs
const page = dv.page("Synced OSCP Notes/Top/Active Machine");const ip = page?.IP ?? "NO IP FOUND";

const command = `ldapsearch -v -x -b "DC=hutch,DC=offsec" -H "ldap://${ip}"`;

dv.paragraph("```bash\n" + command + "\n```");
```
389/tcp   open  ldap          Microsoft Windows Active Directory LDAP (Domain: hutch.offsec, Site: Default-First-Site-Name)