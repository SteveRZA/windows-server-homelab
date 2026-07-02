# Validation Checklist

| Validation Item | Result | Screenshot |
|---|---|---|
| Windows LAPS cmdlet available on DC01 | Success | `01-windows-laps-cmdlet-available.png` |
| Schema extension blocked by permissions (diagnosed) | Informational | `02-schema-update-insufficient-access.png` |
| Schema extension blocked by FSMO/replication (diagnosed) | Informational | `03-schema-update-operation-error.png` |
| DC01 DNS/IPv4 configuration verified | Success | `04-dc01-dns-ipv4-config.png` |
| Schema extension applied successfully | Success | `05-schema-update-applied-successfully.png` |
| LAPS GPO settings configured | Success | `06-laps-gpo-settings-configured.png` |
| LAPS password retrieved from AD (GUI / ADUC) | Success | `07-laps-password-retrieved-aduc-gui.png` |
| LAPS password retrieved from AD (PowerShell, both clients) | Success | `08-laps-password-retrieved-powershell.png` |

## Final Validation Summary

The lab was considered successful because:

- Windows LAPS was confirmed present and its schema extension completed in a
  two-DC forest.
- The blocking issues (Schema Admins membership, invalid FSMO role, broken
  DNS/replication) were identified from event logs and `repadmin`, and resolved.
- The LAPS GPO was configured to manage the built-in Administrator and store the
  password in on-premises Active Directory.
- Computer self-permission was granted on the workstation OU.
- The end-to-end flow was validated on two clients (CLIENT01 and CLIENT02): each
  machine generated a unique, random local administrator password, stored it
  encrypted in AD, and the password was retrieved both via the ADUC LAPS tab and
  via `Get-LapsADPassword`, with decryption authorized to `LAB\Domain Admins`.
- A reporting query was defined to check rotation coverage across all machines.
