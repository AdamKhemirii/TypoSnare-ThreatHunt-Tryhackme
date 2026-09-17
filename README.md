# Typo Snare — Threat Hunt

A small threat-hunting case study from a Windows lab environment.

I followed the activity from the first suspicious download through execution, credential access, lateral movement, Active Directory abuse, and ransomware.

## Case

|Item|Value|
|-|-|
|Host|WKSTN-03.swiftspendfinancial.thm|
|User|SSF\\\\perry.parsons|
|Domain|7zipp.org|
|Initial file|7z2301-x64.msi`|
|Initial time|2023-09-26 14:22:02.685`|
|Sysmon event|15 - FileCreateStreamHash|
|Later payload|777bomb.exe`|
|Later local path|C:\\\\Users\\\\perry.parsons\\\\bomb.exe|
|Later time|2023-09-26 15:41:32.602`|

## Attack chain

```text
Typosquatted download
        |
        v
7z2301-x64.msi
        |
        v
msiexec.exe / temporary payload
        |
        v
PowerShell / IEX
        |
        v
Persistence + DLL execution
        |
        v
Credential dumping
        |
        v
Pass-the-Hash / remote access
        |
        v
Active Directory abuse
        |
        v
777bomb.exe / ransomware
```

## How I investigated

I started with the first useful indicator and kept pivoting on:

`domain -> IP -> host -> user -> process -> parent process -> authentication -> next host`

The main things I looked for were:

* suspicious downloads and network connections
* process creation and parent/child relationships
* PowerShell and IEX activity
* new services and unusual DLL execution
* LSASS access and credential dumping
* NTLM reuse and remote sessions
* privileged group changes
* DCSync and Active Directory discovery
* the final ransomware payload

## Investigation phases

|Phase|Focus|
|-|-|
|01|Initial Access|
|02|Execution|
|03|Persistence / Defense Evasion|
|04|Credential Access|
|05|Lateral Movement|
|06|Active Directory Compromise|
|07|Ransomware Impact|

## Main findings

* `7zipp.org` was used to deliver a look-alike 7-Zip installer.
* The MSI led into a process chain involving `msiexec.exe`, a temporary file, PowerShell/IEX, and `7zlegit.exe`.
* `7zService` provided persistence and `rundll32.exe` was used to execute `7zipp.dll`.
* LSASS was targeted for credential access.
* Recovered credential material was used for Pass-the-Hash and remote access.
* The activity moved from endpoint access into Active Directory abuse.
* The same `7zipp.org` infrastructure appeared again when `777bomb.exe` was downloaded near the end of the attack.

## Detection ideas

The strongest detections are based on sequences, not one filename:

```text
Internet download
    +
MSI execution
    +
PowerShell/IEX
```

```text
New service
    +
Rundll32 loading unusual DLL
```

```text
LSASS access
    +
Credential use for remote authentication
```

```text
Privileged group change
    +
Suspicious remote session
```

```text
Payload download
    +
Rapid file modification / encryption activity
```

## Files

* `investigation/` — phase-by-phase notes
* `iocs/` — indicators and pivots
* `detections/` — detection ideas
* `reports/` — incident summary

## Note

This is a lab-based investigation and portfolio project.

