# 03 — Persistence / Defense Evasion

## What I found

A service named `7zService` was used for persistence. It runs with SYSTEM privileges and gives the attacker execution after reboot.

The next step was:

```text
7zService
   |
   v
rundll32.exe
   |
   v
7zipp.dll
```

PowerShell/IEX was then used again to retrieve another script.

## Why it matters

A new service followed by unusual DLL execution is a good sequence to investigate, especially when it happens on a host that already downloaded a suspicious installer.

## ATT&CK

- T1543.003 — Windows Service
- T1218.011 — Rundll32
- T1059.001 — PowerShell
