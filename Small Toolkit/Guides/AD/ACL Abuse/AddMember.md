You can add another user to a particular AD group.

Add bob to Domain Admins
```
impacket-net 'corp.local/alice:Password123!@DCIP' \
group -name 'Domain Admins' -join 'bob'
```

Windows CMD
```
net group "Domain Admins" alice /add /domain
```

BloodyAD
```
bloodyAD -d corp.local --host <DC_IP> -u alice -p 'Password123!' add groupMember "Domain Admins" "alice"
```