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
