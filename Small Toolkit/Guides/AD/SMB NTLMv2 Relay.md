Lateral movement technique 

**Check SMB Signing Status:**

- **Crucial Rule:** NTLM relaying to SMB **will fail** if SMB signing is _required_ on the target.
- _Recon command:_ Use Impacket's `DumpNTLMInfo.py` or `crackmapexec` / `netexec` to check SMB signing properties across your target subnet:

```
nxc smb 192.168.x.0/24
```

```
nmap -Pn -p445 --script smb2-security-mode <MS02_IP>
```

- Look for hosts where `SMB Signing: False` (or not required). Workstations typically have signing disabled by default, whereas Domain Controllers enforce it globally.