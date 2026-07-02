# Notes

## Why LAPS instead of a shared password

Pushing the same local administrator password to every machine means one
compromised machine exposes local admin on all of them. This is a direct enabler
of lateral movement. LAPS gives every machine a unique, random password stored in
AD, so a single recovered password is useless elsewhere.

## LAPS manages the password, not the account

On this Server 2019 build, LAPS does not create or enable the managed account. It
only sets and rotates the password of an account that already exists and is
enabled. The built-in Administrator exists everywhere but is disabled by default,
so it must be enabled separately.

Enabling it via GPP fails: the GPP password field is blocked (MS14-025), so an
`Update` action applies a blank password and is rejected by the domain password
policy (`0x800708c5`). Startup scripts are fragile. The clean production approach
is to enable the built-in Administrator once in the golden image, so every
deployed machine has it enabled and LAPS takes over the password. Newer Windows
LAPS builds add an "automatic account management" setting that creates and enables
the account too, but it is not present in this build.

## Backup directory must match the join type

The "Configure password backup directory" setting is chosen by machine join type,
not by where you manage from:

- On-prem AD joined or Hybrid Entra joined -> Active Directory
- Entra-only (cloud) joined -> Azure Active Directory

A machine backs up to exactly one directory. A mixed fleet needs separate
policies targeted per OU or group.

## Why the schema step is the hard part

Schema modification is the most privileged operation in AD. It requires:

1. Membership in Schema Admins (and a fresh logon token after being added).
2. A valid Schema Master FSMO role.

The second point caused the main problem in this lab. A powered-off DC02 broke
replication of the Schema partition, which invalidated the FSMO role on DC01,
which in turn blocked the schema write. The lesson: schema failures are often not
about permissions at all - check FSMO validity and replication first.

## Diagnosing "operation error occurred"

The PowerShell exception was generic and unhelpful (empty InnerException). The
real cause was only visible in the `Directory Service` event log (Events 2092 and
2087). When a LAPS/AD cmdlet fails with a vague error, the event log on the DC is
the authoritative source.

## MS14-025 and GPP passwords

Group Policy Preferences can no longer set passwords for local users (the field is
greyed out) because Microsoft disabled it for security reasons in MS14-025. This
is why the custom-account approach needed an initial password it could not supply,
and why the built-in account was the simpler path on this build.
