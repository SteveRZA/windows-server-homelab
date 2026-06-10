# Commands Used - Lab 06

## VBR01 validation

```powershell
hostname
whoami
ipconfig /all
nltest /dsgetdc:lab.local
```

## Create a backup repository folder

The final Veeam default repository path used in this lab was `D:\Backup`, created by Veeam during installation.

If creating a custom repository manually:

```powershell
New-Item -Path "D:\VeeamBackups" -ItemType Directory
```

## Optional connectivity tests

```powershell
ping 192.168.44.2
ping 8.8.8.8
nslookup google.com
Test-NetConnection www.veeam.com -Port 443
```

## Create a restore test file on FS01

```powershell
New-Item -Path "D:\Shares\IT\restore-test.txt" -ItemType File
Set-Content -Path "D:\Shares\IT\restore-test.txt" -Value "This file will be restored from Veeam backup."
```

## Delete the restore test file on FS01

```powershell
Remove-Item -Path "D:\Shares\IT\restore-test.txt"
```

## Validate restored file on FS01

```powershell
Get-ChildItem "D:\Shares\IT"
```

## Validate restored file from CLIENT01

Open the mapped drive or UNC path:

```text
I:\
\\FS01\IT
```
