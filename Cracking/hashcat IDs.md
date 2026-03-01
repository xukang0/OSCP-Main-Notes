**LM hash** → always 32 chars, uppercase hex, `aad3b435b51404eeaad3b435b51404ee` when empty. → `-m 3000`
    
- **NTLM hash** → always 32 chars, lowercase hex, no salt. → `-m 1000`
    
- **NTLMv2 challenge/response** → long string with `:::` and `:` separators. → `-m 5600`
    
- **Kerberos (AS-REP/Roasting)** → starts with `$krb5` etc. → `-m 13100` or `-m 18200` depending.
    
- **Hashes from /etc/shadow** (`$6$...`) → SHA512crypt → `-m 1800`
    
- **MD5 crypt (`$1$...`)** → `-m 500`
    
- **bcrypt (`$2a$...`)** → `-m 3200`

On OSCP, almost all Windows password hashes you see are **NTLM (1000)** — so in practice, you rarely need to count to 60 or more.