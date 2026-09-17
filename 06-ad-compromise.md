# 06 — Active Directory Compromise

## What I found

The activity moved from workstation access into the domain.

The main steps were:

```text
Browser credential theft
        |
        v
AD Recovery group discovery
        |
        v
Privileged account use
        |
        v
anna.jones added to AD Recovery
        |
        v
DCSync activity
        |
        v
SharpHound / AD discovery
        |
        v
damian.hall credential access
        |
        v
Pass-the-Hash
```

## Why it matters

At this point the attacker was no longer focused on a single endpoint. Account control, group membership, replication rights, and domain discovery became the main objectives.

## ATT&CK

- T1555.003 — Credentials from Web Browsers
- T1069.002 — Permission Groups Discovery: Domain Groups
- T1098.007 — Additional Local or Domain Groups
- T1003.006 — DCSync
- T1018 — Remote System Discovery
- T1550.002 — Pass the Hash
