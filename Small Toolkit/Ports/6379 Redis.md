Redis-cli
```dataviewjs
const page = dv.page("Synced OSCP Notes/Top/Active Notes");const ip = page?.IP ?? "NO IP FOUND";

const command = `redis-cli -h ${ip} -p 6379`;

dv.paragraph("```bash\n" + command + "\n```");
```

```
INFO
```

```
KEYS *
```

---

SELECT <db_number>

KEYS (*)

1) key1
2) key2
3) key3

get key2
	it will "cat" the value of key2 out in shell