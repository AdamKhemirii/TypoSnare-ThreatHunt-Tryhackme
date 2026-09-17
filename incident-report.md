# Incident Report

## Summary

The investigation shows a multi-stage compromise that starts with a look-alike software download and ends with ransomware activity across two workstations.

The chain includes:

`Initial Access -> Execution -> Persistence -> Credential Access -> Lateral Movement -> Active Directory Compromise -> Ransomware`

## Main assets

| Asset | Role |
|---|---|
| `WKSTN-03.swiftspendfinancial.thm` | Initial workstation |
| `WKSTN-02` | Secondary workstation |
| `SSF\\perry.parsons` | User tied to the initial activity |
| `anna.jones` | Account involved in password and group changes |
| `damian.hall` | Later credential target |

## Timeline

| Time / stage | Activity |
|---|---|
| 14:22:02.685 | `7z2301-x64.msi` recorded from `7zipp.org` |
| Early stage | MSI execution, temporary payload, PowerShell/IEX |
| Early stage | `7zService` persistence and `7zipp.dll` execution |
| Middle stage | LSASS dumping and credential extraction |
| Middle stage | Pass-the-Hash, WinRM and RDP |
| Later stage | Browser credential theft and AD group changes |
| Later stage | DCSync and further credential access |
| 15:41:32.602 | `777bomb.exe` downloaded to `bomb.exe` |
| Final stage | Ransomware execution and impact |

## What stood out

### 1. The first useful pivot was the download metadata

The ZoneTransfer record connected a local file to an external domain and gave me a clear starting point.

### 2. The process chain was more useful than a single alert

MSI -> temp payload -> PowerShell/IEX -> 7zlegit.exe gives much more context than a PowerShell event by itself.

### 3. Identity activity became more important later

Once credentials were obtained, authentication, remote sessions, group membership and directory replication became key parts of the investigation.

### 4. Infrastructure reuse connected the attack

`7zipp.org` appeared at both the initial delivery stage and the final payload stage.

## Lessons learned

- Start with a strong indicator and pivot from it.
- Always check the parent and child process relationship.
- Treat credential access and lateral movement as connected events.
- Watch for identity changes after endpoint compromise.
- Reused domains and filenames can connect separate stages of an attack.
