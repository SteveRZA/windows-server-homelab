# Commands Used

## Confirm Windows LAPS is available

Run on DC01 as administrator:

```powershell
Get-Command Update-LapsADSchema
```

Confirms the built-in Windows LAPS module is present (`Source: LAPS`).

---

## Extend the AD schema

Run on the Schema Master (DC01) as a member of Schema Admins:

```powershell
Update-LapsADSchema
```

Answer `A` (Yes to All) to add all LAPS attributes. One-time, forest-wide.

---

## Grant computer self-permission

Run on DC01. Grants machines in the OU the right to write their own password:

```powershell
Set-LapsADComputerSelfPermission -Identity "OU=Computers,OU=LAB,DC=lab,DC=local"
```

---

## Enable the built-in Administrator (client side)

LAPS manages the password but does not enable the account on this build. Enable
it once (in the golden image for new machines, or manually on existing ones):

```powershell
net user Administrator /active:yes
```

Note: you cannot set its password manually once LAPS manages it - LAPS controls
the password from the first policy cycle.

---

## Apply policy (client side)

Run on the client as administrator:

```powershell
gpupdate /force
```

LAPS then rotates on its normal policy cycle (or immediately after a reboot).
`Invoke-LapsPolicyProcessing` can force an immediate cycle for testing, but is
not needed in normal operation.

---

## Retrieve the password from AD

Run on DC01 (or any machine with the LAPS module and rights):

```powershell
Get-LapsADPassword -Identity CLIENT02 -AsPlainText
```

Returns the managed account name, current password, expiration, source
(EncryptedPassword), decryption status, and authorized decryptor. The password
can also be read from the **LAPS** tab on the computer object in ADUC.

---

## Report on rotation coverage

Run on DC01:

```powershell
Get-ADComputer -Filter * -Properties msLAPS-PasswordExpirationTime |
  Select Name, @{N="Expires";E={[datetime]::FromFileTime($_."msLAPS-PasswordExpirationTime")}}
```

Shows which machines have a current password and which have not rotated.

---

## Password rotation (day-2 operations)

### Force rotation from the DC (remote, targeted)

```powershell
Set-LapsADPasswordExpirationTime -Identity CLIENT02
```

Marks the password expired (`Status: PasswordReset`). The machine rotates on its
next cycle. `Reset-LapsPassword` does NOT accept `-Identity` - it is local-only.

### Speed up processing on the machine

```powershell
Invoke-LapsPolicyProcessing
```

Forces the machine to process the policy now instead of waiting for the hourly
background task. Requires admin rights, run on the machine.

### Immediate local rotation (on the machine itself)

```powershell
Reset-LapsPassword
```

Rotates the local machine's own password immediately, regardless of expiration.
Intended for rare cases such as a suspected breach.

---

## Recovery

### Retrieve current and previous passwords (history)

```powershell
Get-LapsADPassword -Identity CLIENT02 -AsPlainText -IncludeHistory
```

First recovery tool if the current password does not match the machine. Read it
from the DC, then type it at the client login screen as `.\Administrator`.

### LAPS event log (diagnostics on the machine)

```powershell
Get-WinEvent -LogName "Microsoft-Windows-LAPS/Operational" -MaxEvents 15 |
  Select TimeCreated, Id, LevelDisplayName, Message | Format-List
```

Shows policy processing, rotation attempts, and warnings (e.g. account disabled,
missing schema attribute).

---

## Troubleshooting commands

### Check FSMO / replication (used to diagnose the schema failure)

```powershell
Get-ADForest | Select SchemaMaster
repadmin /showrepl
```

### Force replication of the Schema and Configuration partitions

```powershell
repadmin /replicate DC01 DC02 "CN=Schema,CN=Configuration,DC=lab,DC=local"
repadmin /replicate DC01 DC02 "CN=Configuration,DC=lab,DC=local"
```

### Read the Directory Service event log (revealed the real cause)

```powershell
Get-WinEvent -LogName "Directory Service" -MaxEvents 15 |
  Select TimeCreated, Id, LevelDisplayName, Message | Format-List
```

### Add account to Schema Admins (requires logoff/reboot to take effect)

```powershell
Add-ADGroupMember "Schema Admins" -Members <SamAccountName>
whoami /groups | findstr /i "schema"
```
