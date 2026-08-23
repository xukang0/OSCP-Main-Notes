Swiss Army Knife for SMTP
```dataviewjs
const page = dv.page("Synced OSCP Notes/Top/Active Machine");const ip = page?.IP ?? "NO IP FOUND";

const command = `sudo swaks -t [target@localhost] --from [sender@localhost] --attach @file.ods --server ${ip} --body "My message to you" --header "Subject: Please check this spreadsheet"`;

dv.paragraph("```bash\n" + command + "\n```");
```

Use cases : Phishing attack to admin email with LibreOffice ODS or ODT attachment [[Malicious Macro Generator LibreOffice or OpenOffice ODT ODS]]

[[Phishing]] for non office attachments