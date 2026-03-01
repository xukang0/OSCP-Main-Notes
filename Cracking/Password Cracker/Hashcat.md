```
hashid [hash]
```

![[Pasted image 20250528033219.png]]


```
echo [hash] > hash
```

```
hashcat -a 0 -m 0 [hash] /usr/share/wordlists/rockyou.txt
```

```
hashcat -m 5600 hash /usr/share/wordlists/rockyou.txt
```
### 🔹 Common relevant Hashcat codes for SQL/Windows

HASHCAT CODES
https://hashcat.net/wiki/doku.php?id=example_hashes

|Hashcat code|Type|
|---|---|
|1000|NTLM|
|5500|NetNTLMv1|
|5600|NetNTLMv2 / MS SQL 2005+|
|13100|Kerberos 5 AS-REP|
|13800|Kerberos 5 TGS-REP|
Rules

```
hashcat -a 0 -m 0 [hash] /usr/share/wordlists/rockyou.txt -r /usr/share/hashcat/rules/best64.rule
```

List Rules

```
ls -l /usr/share/hashcat/rules
```

Masks

| Symbol | Charset                             |
| ------ | ----------------------------------- |
| ?l     | abcdefghijklmnopqrstuvwxyz          |
| ?u     | ABCDEFGHIJKLMNOPQRSTUVWXYZ          |
| ?d     | 0123456789                          |
| ?h     | 0123456789abcdef                    |
| ?H     | 0123456789ABCDEF                    |
| ?s     | «space»!"#$%&'()*+,-./:;<=>?@[]^_`{ |
| ?a     | ?l?u?d?s                            |
| ?b     | 0x00 - 0xff                         |

```
hashcat -a 3 -m 0 [hash] '?u?l?l?l?l?d?s'
```

![[Pasted image 20250528033339.png]]

Creating custom crack list

```
hashcat --stdout \  
-a 1 \  
mark_initial.txt \  
mark_initial.txt \  
> mark_pairs.txt
```

Combine 2 word as combinations

Only keep those with 12 characters or longer

```
awk 'length($0) >= 12' mark_pairs.txt > pairs_length12.txt
```

Word count

```
wc -l pairs_length12.txt  
76
```

Custom Rule

```
cat << 'EOF' > custom.rule  
:  
c  
so0  
c so0  
sa@  
c sa@  
c sa@ so0  
$!  
$! c  
$! so0  
$! sa@  
$! c so0  
$! c sa@  
$! so0 sa@  
$! c so0 sa@  
EOF
```

This rule set covers a range of transformations, including:

- Capitalizing the first letter (`c`)
- Substituting `a` with `@` (`sa@`)
- Substituting `o` with `0` (`so0`)
- Appending `!` to the end (`$!`)
- Various combinations of these

Combine Everything

```
hashcat --stdout \  
-r custom.rule \  
pairs_length12.txt \  
> mut_mark_final.txt
```

Analyse hash type 

```
hashid -m [hash]
```

Run

```
hashcat -a 0 -m 0 [hash] /home/kali/Desktop/mut_mark_final.txt
```

- `-a 0`: straight wordlist attack mode
- `-m 0`: specifies MD5 hash mode
- The final wordlist path points to our custom file