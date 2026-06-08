# Notes - Lab 04

## Why a dedicated file server?

A Domain Controller should primarily provide identity, authentication, DNS, and directory services. Hosting department file shares on a separate file server is a cleaner and more realistic design.

## Why use a second disk?

The operating system is kept on `C:` and shared data is stored on `D:`. This separation improves organization and prepares the lab for future backup, quota, and storage management labs.

## Why use SG and DL groups?

Department groups identify user roles:

```text
SG_IT_Users
SG_HR_Users
SG_Finance_Users
```

Resource permission groups identify access to folders:

```text
DL_FS_IT_Modify
DL_FS_HR_Modify
DL_FS_Finance_Modify
DL_FS_Public_Modify
```

This creates a clean access model:

```text
User → Department Group → Permission Group → Folder Permission
```

## Why use GPO mapped drives?

NTFS permissions control access. GPO mapped drives improve user experience by automatically showing the correct network drives after login.

Example:

```text
IT users see I: and P:
HR users see H: and P:
Finance users see F: and P:
```

## Optional next validation

Create a new domain user, add the user to the correct department group, log in from `CLIENT01`, and confirm that the correct mapped drives appear automatically.
