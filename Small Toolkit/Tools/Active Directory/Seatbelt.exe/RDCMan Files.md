The `RDCManFiles` command searches for Remote Desktop Connection Manager (RDCMan) configuration files on the system. RDCMan is a Microsoft tool for managing multiple RDP connections, and its .rdg files contain server lists, connection settings, and sometimes stored credentials.

```powershell
.\seatbelt.exe CredEnum RDCManFiles outputfile="C:\Users\eric.wallows\Documents\seatbelt-targeted.txt"
```