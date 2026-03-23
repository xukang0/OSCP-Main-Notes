### **465 → SMTPS**

- Service: SMTPS
- SMTP over SSL

👉 Possible angles:

- user enumeration
- misconfig mail server

Try:


```
openssl s_client -connect 10.129.224.168:465
```
