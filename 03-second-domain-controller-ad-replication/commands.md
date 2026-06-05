# Commands Used - Lab 03

## DC02 Identity Check

```powershell
hostname
```

Used to confirm that the server was renamed correctly to `DC02`.

---

## List Domain Controllers

```powershell
Get-ADDomainController -Filter *
```

Used to verify that both `DC01` and `DC02` are registered as Domain Controllers in the `lab.local` domain.

---

## FSMO Role Check

```cmd
netdom query fsmo
```

Used to confirm that FSMO roles remain assigned to `DC01.lab.local`.

---

## Replication Summary

```cmd
repadmin /replsummary
```

Used to check overall replication health between Domain Controllers.

Expected result:

```text
fails/total = 0
```

---

## Detailed Replication Status

```cmd
repadmin /showrepl
```

Used to verify successful inbound replication from `DC01` to `DC02`.

---

## DNS Validation

```cmd
nslookup dc01.lab.local
nslookup dc02.lab.local
```

Used to confirm that DNS records exist for both Domain Controllers.

---

## RID Manager Validation

```cmd
dcdiag /test:ridmanager /v
```

Used to confirm that `DC02` can contact the RID Master and pass the RID Manager test.

Expected successful output includes:

```text
DC02 passed test RidManager
```

---

## Domain Controller Health Check

```cmd
dcdiag /q
```

Used to show only current errors. No output means no current errors were detected.

---

## Client DNS Configuration Check

```cmd
ipconfig /all
```

Used on `CLIENT01` to confirm both Domain Controllers are configured as DNS servers:

```text
192.168.44.10
192.168.44.11
```

---

## Client DNS Resolution Test

```cmd
nslookup dc01.lab.local
nslookup dc02.lab.local
nslookup google.com
```

Used to verify that the client can resolve both internal AD records and external internet records.

---

## Client Domain Controller Discovery

```cmd
nltest /dsgetdc:lab.local
```

Used to confirm that `CLIENT01` can discover a Domain Controller for the `lab.local` domain.
