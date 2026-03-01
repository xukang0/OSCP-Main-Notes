## 🔍 Full Command:

```dataviewjs
const page = dv.page("Templater/IP");const ip = page?.IP ?? "NO IP FOUND";

const command = `snmpwalk -v2c -c backup ${ip}`

dv.paragraph("```bash\n" + command + "\n```");
```

---

### ✅ `-v 2c`

This specifies the **SNMP version**:

- `-v 1`: Use SNMP version 1
    
- `-v 2c`: Use SNMP version 2c (common & more capable than v1)
    
- `-v 3`: Use SNMP v3 (more secure but rare in misconfigurations)
    

**We use `2c`** because it's widely used and often misconfigured with open `public` access.

---

### ✅ `-c public`

This is the **community string**, which acts like a "password" for SNMP v1/v2c.

- Default is usually `public`
    
- Acts like a "read-only password"
    
- If wrong, you won't get any response or data
    

If the target uses a different string (e.g., `private`), you’ll need to guess or brute-force it.

---

### ✅ `1.3.6.1.2.1.1.4.0`

This is the **OID** (Object Identifier), which tells SNMP what specific data you want.

This particular one is:

- `sysContact.0` — often contains the admin's email or contact name
    

---

## 🧠 Summary:

|Option|Meaning|
|---|---|
|`-v 2c`|Use SNMP version 2c|
|`-c public`|Use community string “public” (default)|
|`1.3.6.1.2.1.1.4.0`|Ask for the sysContact field (admin email)|