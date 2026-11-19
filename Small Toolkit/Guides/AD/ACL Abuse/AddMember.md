You can add another user to a particular AD group.

Add bob to Domain Admins
```
impacket-net 'corp.local/alice:Password123!@DCIP' \
group -name 'Domain Admins' -join 'bob'
```