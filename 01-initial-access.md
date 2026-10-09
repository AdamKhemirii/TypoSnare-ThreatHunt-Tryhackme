# 01 — Initial Access

## What I found

The first strong lead was a Windows ZoneTransfer entry for a file downloaded from a look-alike 7-Zip domain.

```text
[ZoneTransfer]
ZoneId=3
HostUrl=http://www.7zipp.org/a/7z2301-x64.msi
```

The event was on `WKSTN-03.swiftspendfinancial.thm` under `SSF\\perry.parsons`.

**Time:** `2023-09-26 14:22:02.685`

**Sysmon:** Event ID `15` — `FileCreateStreamHash`

- ZoneId 3 shows that Windows marked the file as coming from the Internet. The domain also looks intentionally close to a legitimate software domain, so the download is a useful starting point for the hunt.

## ATT&CK

- T1204.002 — User Execution: Malicious File
