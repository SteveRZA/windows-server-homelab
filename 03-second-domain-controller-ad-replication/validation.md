# Validation - Lab 03

## Validation Checklist

| Check | Command / Tool | Expected Result | Status |
|---|---|---|---|
| Confirm hostname | `hostname` | `DC02` | Passed |
| Confirm both DCs exist | `Get-ADDomainController -Filter *` | `DC01` and `DC02` listed | Passed |
| Confirm FSMO roles | `netdom query fsmo` | All FSMO roles on `DC01.lab.local` | Passed |
| Check replication summary | `repadmin /replsummary` | `0` failures | Passed |
| Check detailed replication | `repadmin /showrepl` | Successful replication attempts | Passed |
| Resolve DC01 | `nslookup dc01.lab.local` | `192.168.44.10` | Passed |
| Resolve DC02 | `nslookup dc02.lab.local` | `192.168.44.11` | Passed |
| Check RID Manager | `dcdiag /test:ridmanager /v` | `DC02 passed test RidManager` | Passed |
| Check current DC health | `dcdiag /q` | No output | Passed |
| Confirm client dual DNS | `ipconfig /all` on `CLIENT01` | DNS servers include `192.168.44.10` and `192.168.44.11` | Passed |
| Confirm client DNS resolution | `nslookup` tests | Internal and external records resolve | Passed |
| Confirm client DC discovery | `nltest /dsgetdc:lab.local` | Domain Controller returned successfully | Passed |
| Confirm AD replication visually | ADUC on `DC02` | `LAB` OU structure visible | Passed |

---

## Important Validation Notes

### Replication

`repadmin /replsummary` showed zero replication failures between `DC01` and `DC02`.

`repadmin /showrepl` showed successful inbound replication from `DC01` to `DC02`.

### FSMO Roles

The FSMO roles were intentionally left on `DC01`:

```text
Schema master
Domain naming master
PDC
RID pool manager
Infrastructure master
```

This is expected. Adding a second Domain Controller does not automatically move FSMO roles.

### DCDIAG SystemLog Events

`dcdiag /q` initially reported System Log warnings related to previous setup activity. The core AD checks were validated separately:

- Replication passed
- RID Manager passed
- DNS resolution passed
- Domain Controller discovery passed

After clearing old System Log events, `dcdiag /q` returned no current errors.

### DNS Redundancy

`CLIENT01` was configured to use both Domain Controllers as DNS servers:

```text
192.168.44.10
192.168.44.11
```

This allows the client to continue resolving AD DNS records if one Domain Controller/DNS server is unavailable.
