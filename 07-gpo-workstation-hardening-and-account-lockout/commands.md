# Commands Used

## Apply Group Policy

```cmd
gpupdate /force
```

Used after configuring or modifying Group Policy settings.

---

## Validate Computer GPOs

Run from CLIENT01 as administrator:

```cmd
gpresult /r /scope computer
```

Used to confirm that `GPO_Workstation_Hardening_Computer` applied to CLIENT01.

---

## Validate User GPOs

Run as the standard user `john.it`.

Because Command Prompt was blocked by policy, PowerShell was used:

```powershell
gpresult /r /scope user
```

Used to confirm that `GPO_User_Restrictions_Standard_Users` applied to `john.it`.

---

## Validate Domain Account Lockout Policy

Run on DC01 as administrator:

```cmd
gpupdate /force
net accounts /domain
```

Expected lockout values:

```text
Lockout threshold: 5
Lockout duration (minutes): 15
Lockout observation window (minutes): 15
```
