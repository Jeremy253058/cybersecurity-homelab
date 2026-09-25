# Detection — Multiple failed logons

## Objective

Detect a concentration of Windows Security Event ID 4625 events that may indicate repeated authentication failures against the same account or from the same source IP.

## Lab threshold

The current AD lockout policy is:

- LockoutThreshold: 5
- LockoutDuration: 15 minutes
- LockoutObservationWindow: 15 minutes

The detection below uses the same 5-event / 15-minute window as a lab baseline. This is a detection threshold, not proof that an attack is occurring.

## PowerShell query

Run on SRV25:

~~~powershell
$events=Get-WinEvent -FilterHashtable @{LogName='Security';Id=4625;StartTime=(Get-Date).AddMinutes(-15)}; $rows=$events|ForEach-Object {[xml]$x=$_.ToXml();$d=@{};$x.Event.EventData.Data|ForEach-Object {$d[$_.Name]=$_. '#text'};[PSCustomObject]@{Time=$_.TimeCreated;User=$d.TargetUserName;IP=$d.IpAddress;Status=$d.Status;SubStatus=$d.SubStatus}}; $rows|Group-Object User,IP|Where-Object Count -ge 5|Sort-Object Count -Descending|Select-Object Count,Name
~~~

## Interpretation

A result with Count >= 5 means that at least five Event ID 4625 records were observed for the same User + IP pair during the last 15 minutes.

This should trigger investigation of:

- targeted account;
- source IP;
- authentication package;
- logon type;
- status/substatus;
- whether the account became locked;
- whether successful authentication followed the failures.

## False positives

- User repeatedly entering an incorrect password.
- A service or scheduled task using stale credentials.
- A misconfigured application.
- Administrative scripts using outdated credentials.

## Response workflow

1. Validate the source IP.
2. Identify the targeted account.
3. Review the corresponding 4625 events.
4. Check for account lockout events.
5. Check for a successful logon after the failures.
6. Determine whether the activity is expected or requires incident response.

## Observed lab test — 2026-09-25

A dedicated test account `redteam-test` was used for the controlled authentication-failure scenario.

Observed sequence:

- AD lockout threshold: 5 failures.
- `BadPwdCount` reached 5.
- `LockedOut` became `True`.
- Five Event ID 4625 records were observed in close succession.
- A direct search for Event ID 4740 immediately afterward did not return a result in the queried Security log.

The absence of a returned 4740 in that query should not be interpreted as proof that no lockout event exists anywhere in the environment. The event can be investigated further using the domain-controller security logs and the event timestamp.

The scenario therefore confirms the following chain in the lab:

```text
Kali / redteam-test
        |
        | repeated incorrect SMB authentication
        v
SRV25 / Active Directory
        |
        +--> Event ID 4625 (failed logon)
        |
        +--> BadPwdCount = 5
        |
        +--> LockedOut = True
```

The account should not be used for additional authentication attempts while it remains locked.
