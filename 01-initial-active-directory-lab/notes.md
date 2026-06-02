# Lab Notes

## What Went Well

- Domain controller was successfully configured for `lab.local`.
- DNS records for the domain controller and client were created.
- NTP synchronization was configured and validated.
- File shares were created and secured using AD security groups.
- A mapped drive was deployed using Group Policy Preferences.
- The client received the mapped drive successfully after Group Policy processing.

## Lessons Learned

- NTFS permissions should be assigned to groups, not directly to users.
- Final file access is affected by both Share Permissions and NTFS Permissions.
- AD depends heavily on DNS, so DNS validation is important.
- User-side GPOs must be tested while logged in as the target domain user.
- `gpresult /r` is useful for confirming which GPOs were applied.

## Improvement for Next Lab

The next version of the lab should separate server roles:

```text
DC01  - Domain Controller / DNS / NTP
FS01  - File Server
CLIENT01 - Domain Client
```

This will better match a real small-business or enterprise-style environment.
