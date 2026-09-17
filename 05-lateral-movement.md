# 05 — Lateral Movement

## What I found

Recovered NTLM material was used for Pass-the-Hash. Remote access followed through WinRM and later RDP.

The WinRM session showed `wsmprovhost.exe`, and repeated `whoami` commands were used during the session.

The RDP activity included normal session processes such as:

- `winlogon.exe`
- `LogonUI.exe`
- `rdpclip.exe`
- `AtBroker.exe`

Sticky Keys manipulation was then used during the RDP phase.

## Why it matters

A remote authentication event becomes much more interesting when it is followed by unusual process execution or privilege-related changes.

## ATT&CK

- T1550.002 — Pass the Hash
- T1021.006 — Windows Remote Management
- T1021.001 — Remote Desktop Protocol
- T1546.008 — Accessibility Features
