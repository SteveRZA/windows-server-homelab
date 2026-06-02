# Commands Used

## Domain / Client Validation

```cmd
hostname
ipconfig /all
whoami
whoami /fqdn
```

## DNS Validation

```cmd
nslookup dc01.lab.local
ping dc01.lab.local
```

## Group Policy Validation

```cmd
gpupdate /force
gpresult /r
whoami /groups
```

## NTP Configuration

```cmd
w32tm /config /manualpeerlist:"time.windows.com,0x8" /syncfromflags:manual /reliable:yes /update
net stop w32time
net start w32time
w32tm /resync
```

## NTP Validation

```cmd
w32tm /query /status
w32tm /query /source
```

## Useful Domain Controller Checks

```cmd
netdom query fsmo
dcdiag
```

## Useful PowerShell Checks

```powershell
Get-ADDomain
Get-ADForest
Get-ADUser -Filter *
Get-ADGroup -Filter *
```
