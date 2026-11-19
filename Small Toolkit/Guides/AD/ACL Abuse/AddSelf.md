You can add yourself to a particular group, but you cannot necessarily add arbitrary users.

```
impacket-net 'corp.local/alice:Password123!@10.10.10.10' group -name 'TargetGroup' -join 'alice'
```