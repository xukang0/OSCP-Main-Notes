161
162
10161
10162

---

SNMP Bulkwalk Enumeration
```dataviewjs
const page = dv.page("Synced OSCP Notes/Top/Active Machine");const ip = page?.IP ?? "NO IP FOUND";

const command = `snmpbulkwalk -c [COMM_STRING] -v [VERSION] ${ip} .`;

dv.paragraph("```bash\n" + command + "\n```");
```
```
snmpbulkwalk -c public -v2c 10.10.11.136 .
```

---

SNMP Check Enumeration
```dataviewjs
const page = dv.page("Synced OSCP Notes/Top/Active Machine");const ip = page?.IP ?? "NO IP FOUND";

const command = `snmp-check ${ip} -c public`;

dv.paragraph("```bash\n" + command + "\n```");
```
