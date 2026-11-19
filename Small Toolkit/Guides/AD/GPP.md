cPassword

we can use `gpp-decrypt` which uses AES-256 key to decrypt the data. `gpp-decrypt` is a utility specifically designed to decrypt the `cPassword` (or "cipher-password") attribute found in Group Policy Preferences (GPP) XML files on a Windows domain.

```
gpp-decrypt [hash]
```

---

```
grep -ri "cpassword" .
```

```
gpp-decrypt '<CPASSWORD>'
```