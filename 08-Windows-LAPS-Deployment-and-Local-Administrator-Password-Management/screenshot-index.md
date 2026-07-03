# Screenshot Index

| File | Description |
|---|---|
| `01-windows-laps-cmdlet-available.png` | `Get-Command Update-LapsADSchema` resolving with `Source: LAPS`, confirming built-in Windows LAPS is present |
| `02-schema-update-insufficient-access.png` | First `Update-LapsADSchema` attempt failing with "insufficient access rights" (Schema Admins required) |
| `03-schema-update-operation-error.png` | Second attempt failing with "An operation error occurred" (caused by invalid Schema Master FSMO role) |
| `04-dc01-dns-ipv4-config.png` | DC01 IPv4/DNS configuration - preferred DNS pointing to itself, alternate to DC02 |
| `05-schema-update-applied-successfully.png` | `Update-LapsADSchema` completing successfully after replication was restored |
| `06-laps-gpo-settings-configured.png` | LAPS GPO with backup directory, administrator account name, and password settings all Enabled |
| `07-laps-password-retrieved-aduc-gui.png` | LAPS tab in ADUC showing CLIENT02's managed account name, current password, and expiration date |
| `08-laps-password-retrieved-powershell.png` | `Get-LapsADPassword` output for CLIENT01 and CLIENT02, each with a unique password, EncryptedPassword source, and successful decryption |
| `09-rotation-before.png` | `Get-LapsADPassword` before rotation - current password and update time |
| `10-rotation-expire-triggered.png` | `Set-LapsADPasswordExpirationTime` forcing expiration from the DC (`Status: PasswordReset`) |
| `11-rotation-invoke-processing.png` | `Invoke-LapsPolicyProcessing` run on the client to process the policy immediately |
| `12-rotation-after.png` | `Get-LapsADPassword` after rotation - new password and new update timestamp (before/after proof) |
