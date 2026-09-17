# Detection Ideas

## Internet-origin MSI followed by execution

Look for an Internet-downloaded MSI that is executed shortly after it appears on the host.

Useful fields:

`host.name`, `user.name`, `file.name`, `process.name`, `process.parent.name`, timestamp

## PowerShell downloading an executable

Look for PowerShell using `iwr`, `Invoke-WebRequest`, or similar download behavior and writing an `.exe` into a user directory.

## Suspicious service creation

Alert on new services with unusual names, locations, or binaries, especially when the same host already shows suspicious PowerShell or MSI activity.

## Rundll32 loading an unusual DLL

Look for `rundll32.exe` loading DLLs from temporary or user-writable locations.

## LSASS access

Watch for unusual processes accessing LSASS or creating memory dumps around the same time as credential-access activity.

## Pass-the-Hash

Correlate unusual NTLM authentication with a new remote session and suspicious child processes.

## Privileged group changes

Alert when a workstation-originated session changes membership of a sensitive domain group.

## DCSync

Monitor for directory replication requests coming from accounts or systems that do not normally perform replication.

## Ransomware chain

A useful sequence is:

```text
payload download
      +
remote execution
      +
burst of file changes
```
