SMTP and IMAP are usually open together
SMTP is the delivery truck, IMAP is the mailbox.
[[143 993 IMAP]]

Connect
```dataviewjs
const page = dv.page("Synced OSCP Notes/Top/Active Machine");const ip = page?.IP ?? "NO IP FOUND";

const command = `telnet ${ip} 25`;

dv.paragraph("```bash\n" + command + "\n```");
```
brute force usernames
```dataviewjs
const page = dv.page("Synced OSCP Notes/Top/Active Machine");const ip = page?.IP ?? "NO IP FOUND";

const command = `smtp-user-enum -M RCPT -U /usr/share/wordlists/footprinting-wordlist.txt -t ${ip}`;

dv.paragraph("```bash\n" + command + "\n```");
```

```
cat smtp_usernames.txt
```

Gather possible usernames on all available resources and check for availability with enum script.
```dataviewjs
const page = dv.page("Synced OSCP Notes/Top/Active Machine");const ip = page?.IP ?? "NO IP FOUND";

const command = `smtp-user-enum -M VRFY -D postfish.off -U Users.txt -t ${ip}`;

dv.paragraph("```bash\n" + command + "\n```");
```


| **Command**  | **Description**                                                                                  |
| ------------ | ------------------------------------------------------------------------------------------------ |
| `AUTH PLAIN` | AUTH is a service extension used to authenticate the client.                                     |
| `HELO`       | The client logs in with its computer name and thus starts the session.                           |
| `MAIL FROM`  | The client names the email sender.                                                               |
| `RCPT TO`    | The client names the email recipient.                                                            |
| `DATA`       | The client initiates the transmission of the email.                                              |
| `RSET`       | The client aborts the initiated transmission but keeps the connection between client and server. |
| `VRFY`       | The client checks if a mailbox is available for message transfer.                                |
| `EXPN`       | The client also checks if a mailbox is available for messaging with this command.                |
| `NOOP`       | The client requests a response from the server to prevent disconnection due to time-out.         |
| `QUIT`       | The client terminates the session.                                                               |


Bigger Scan
```dataviewjs
const page = dv.page("Synced OSCP Notes/Top/Active Machine");const ip = page?.IP ?? "NO IP FOUND";

const command = `smtp-user-enum -M VRFY -U /usr/share/wordlists/metasploit/namelist.txt -t ${ip}`;

dv.paragraph("```bash\n" + command + "\n```");
```
---

```powershell
nc -nv 192.168.53.137 25  

(UNKNOWN) [192.168.53.137] 25 (smtp) open  

220 postfish.off ESMTP Postfix (Ubuntu)  

MAIL FROM: it@postfish.off  

250 2.1.0 Ok  

RCPT TO: brian.moore@postfish.off  

250 2.1.5 Ok  

DATA  

354 End data with <CR><LF>.<CR><LF>  

hi  
.  

250 2.0.0 Ok: queued as 0D913458E8  

QUIT  
221 2.0.0 Bye
```