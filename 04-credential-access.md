# 04 — Credential Access

## What I found

The next phase targeted LSASS memory.

```text
rundll32.exe
      |
      v
Invoke-NanoDump.ps1
      |
      v
LSASS dump
      |
      v
WerFault.exe process snapshot
      |
      v
pwrex.ps1 / PowerExtract
```

The investigation also showed the LSASS dump being saved with a misleading `.evtx` extension before credential extraction.

## Why it matters

The important signal is not a single tool name. It is the combination of unusual LSASS access, dump activity, and later use of the recovered credentials.

## ATT&CK

- T1003.001 — LSASS Memory
