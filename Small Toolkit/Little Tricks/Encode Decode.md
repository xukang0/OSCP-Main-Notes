```
echo "HASH" | base64 -d
```

URL Encode 
https://www.url-encode-decode.com/

Patterns

| Encoded | Real |
| ------- | ---- |
| %2F     | /    |
|         |      |

## Windows Powershell Base64 Encode

```
[Convert]::ToBase64String([IO.File]::ReadAllBytes('C:\Users\steph.cooper\appdata\Roaming\Microsoft\Credentials\C8D69EBE9A43E9DEBF6B5FBD48B521B9'))
```