## Check Pre-Auth As-rep Kerberoasting

 Why Scan for Pre-Authentication?

Normally, Kerberos uses **Pre-Authentication** to prevent password guessing:

1. When a user requests a ticket (AS-REQ), Kerberos requires them to encrypt the current timestamp using a key derived fr their password.
2. The Domain Controller (DC) decrypts it. If correct, the DC knows the user has the password and issues a Ticket Granting Ticket (TGT).

However, if an account has the setting **"Do not require Kerberos pre-authentication"** (`DONT_REQ_PREAUTH`) enabled in Active Directory:

- Anyone can send an AS-REQ to the DC asking for an authentication ticket on behalf of that username.
- Because pre-authentication is turned off, the DC **immediately sends back an AS-REP response** containing an encrypted ticket payload.
- That payload is encrypted with the target user's password hash.

The AS-REP (Authentication Server Response) is an encrypted Kerberos Ticket-Granting Ticket (TGT) for a user account whose Kerberos pre-authentication is disabled.

```dataviewjs
const page = dv.page("Synced OSCP Notes/Top/Active Machine");
const discoveredDomain = page?.["Discovered Web Domain"] ?? "NO DOMAIN FOUND";const ip = page?.IP ?? "NO IP FOUND";

const command = `impacket-GetNPUsers -request -usersfile users ${discoveredDomain}/ -dc-ip ${ip}`;

dv.paragraph("```bash\n" + command + "\n```");
```

```
impacket-GetNPUsers DOMAIN/ -usersfile users.txt -dc-ip <DC_IP>
```