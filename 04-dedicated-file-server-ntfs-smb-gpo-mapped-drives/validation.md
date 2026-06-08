# Validation - Lab 04

## 1. FS01 static IP and DNS

Validated that `FS01` uses a static IP address and points to both Domain Controllers for DNS.

Expected configuration:

```text
IP Address: 192.168.44.20
Gateway: 192.168.44.2
DNS 1: 192.168.44.10
DNS 2: 192.168.44.11
```

Screenshot:

```text
screenshots/01-fs01-static-ip-config.png
```

---

## 2. FS01 domain join and Group Policy

Validated that `FS01` is domain joined, can discover a Domain Controller, and receives domain Group Policy.

Screenshots:

```text
screenshots/02-fs01-domain-controller-discovery.png
screenshots/04-fs01-gpresult-server-ou-domain-admin.png
```

---

## 3. File Server role

Validated that the File Server role was installed on `FS01`.

Screenshot:

```text
screenshots/05-fs01-file-server-role-installed.png
```

---

## 4. Folder structure

Validated the folder structure on the dedicated data disk.

```text
D:\Shares
├── IT
├── HR
├── Finance
└── Public
```

Screenshot:

```text
screenshots/06-fs01-share-folder-structure.png
```

---

## 5. AD group and nesting model

Validated that file server permission groups exist and that department groups are nested inside permission groups.

Screenshots:

```text
screenshots/07-ad-file-server-permission-groups.png
screenshots/08-permission-group-nesting-example.png
```

---

## 6. NTFS permissions

Validated that IT folder permissions use the expected ACL model.

Expected IT ACL:

```text
SYSTEM: Full Control
Administrators: Full Control
DL_FS_IT_Modify: Modify
```

Screenshot:

```text
screenshots/09-ntfs-permissions-it-folder-advanced.png
```

---

## 7. SMB shares

Validated that the following SMB shares were created:

```text
\\FS01\IT
\\FS01\HR
\\FS01\Finance
\\FS01\Public
```

Screenshot:

```text
screenshots/11-all-smb-shares-created.png
```

---

## 8. Client access test

Validated with an IT user.

| Test | Expected Result | Actual Result |
|---|---|---|
| Access `\\FS01\IT` | Allowed | Passed |
| Create file in `\\FS01\IT` | Allowed | Passed |
| Access `\\FS01\HR` | Denied | Passed |

Screenshots:

```text
screenshots/12-client-it-user-access-it-share.png
screenshots/13-client-it-user-denied-hr-share.png
```

---

## 9. GPO mapped drives

Validated that `GPO_Mapped_Drives_FS01` applied to user `john.it`.

Expected mapped drives:

```text
I: → \\FS01\IT
P: → \\FS01\Public
```

Screenshots:

```text
screenshots/16-gpresult-mapped-drives-gpo-applied.png
screenshots/17-client01-it-user-mapped-drives.png
```
