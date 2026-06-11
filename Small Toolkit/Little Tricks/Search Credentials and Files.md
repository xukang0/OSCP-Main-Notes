## Search Creds

```
grep -ri "PASSWORD" / 2>/dev/null | grep "DB"
```

```
grep -ri "PASSWORD" / 2>/dev/null | grep "$DB['PASSWORD']"
```
## Search interesting files

```
find / -type f \( -name "*.conf" -o -name "*.config" -o -name "*.php" -o -name "*.sql" -o -name "*.db" -o -name "*.env" -o -name "*settings*" \) 2>/dev/null
```

Pinpoint directories to reduce noise

```
find /var/www/ /etc/ /opt/ -type f \( -name "*.conf*" -o -name "*.env" \) 2>/dev/null
```

One Condition
```
find / -type f -name "*.php" 2>/dev/null
```

Double Condition
```
find / -type f \( -name "*.php" -o -name "*.conf" \) 2>/dev/null
```

List

.conf
.config
.sql
.db
.php
.env

## Search Flags

Local.txt
```
find / -iname local.txt -type f 2>/dev/null
```

Local.txt
```
find / -iname proof.txt -type f 2>/dev/null
```