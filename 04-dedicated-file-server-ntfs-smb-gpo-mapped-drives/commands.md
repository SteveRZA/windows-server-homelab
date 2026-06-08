# Commands - Lab 04

## FS01 network and domain validation

```cmd
ipconfig /all
whoami
hostname
nltest /dsgetdc:lab.local
gpresult /r
```

## Folder creation

```powershell
New-Item -Path "D:\Shares" -ItemType Directory
New-Item -Path "D:\Shares\IT" -ItemType Directory
New-Item -Path "D:\Shares\HR" -ItemType Directory
New-Item -Path "D:\Shares\Finance" -ItemType Directory
New-Item -Path "D:\Shares\Public" -ItemType Directory
```

## Example NTFS permission configuration with icacls

```powershell
icacls "D:\Shares\IT" /inheritance:r
icacls "D:\Shares\IT" /grant "SYSTEM:(OI)(CI)(F)"
icacls "D:\Shares\IT" /grant "Administrators:(OI)(CI)(F)"
icacls "D:\Shares\IT" /grant "LAB\DL_FS_IT_Modify:(OI)(CI)(M)"
```

Repeat the same model for the other folders:

```powershell
icacls "D:\Shares\HR" /grant "LAB\DL_FS_HR_Modify:(OI)(CI)(M)"
icacls "D:\Shares\Finance" /grant "LAB\DL_FS_Finance_Modify:(OI)(CI)(M)"
icacls "D:\Shares\Public" /grant "LAB\DL_FS_Public_Modify:(OI)(CI)(M)"
```

## Client validation

```cmd
gpupdate /force
gpresult /r
whoami
```

Manual access tests:

```text
\\FS01\IT
\\FS01\HR
\\FS01\Finance
\\FS01\Public
```
