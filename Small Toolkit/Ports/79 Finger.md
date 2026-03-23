### **79 → Finger**

- Service: Finger
- Purpose:
    - Shows logged-in users
    - Can reveal usernames, home dirs, shells
-
```dataviewjs
const page = dv.page("Synced OSCP Notes/Top/Active Notes");const ip = page?.IP ?? "NO IP FOUND";

const command = `finger @${ip}`;

dv.paragraph("```bash\n" + command + "\n```");
```
