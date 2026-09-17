# 02 — Execution

## What I found

The MSI starts the next part of the chain. The activity I traced is:

```text
7z2301-x64.msi
    |
    v
msiexec.exe
    |
    v
MSI542E.tmp
    |
    v
PowerShell / IEX
    |
    v
7zlegit.exe
```

`7zlegit.exe` is especially interesting because the name makes the process look like normal 7-Zip activity.

## Why it matters

PowerShell by itself is common. The more useful signal is the full process chain and the context around it.

## ATT&CK

- T1218.007 — Msiexec
- T1059.001 — PowerShell
- T1036.005 — Match Legitimate Name or Location
