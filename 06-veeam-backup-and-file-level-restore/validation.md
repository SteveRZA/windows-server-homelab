# Validation - Lab 06

## VBR01 validation

Confirmed:

```text
Hostname: VBR01
Domain user: LAB\lab.admin
IP address: 192.168.44.30
DNS servers: 192.168.44.10, 192.168.44.11
Domain Controller discovery: DC01.lab.local
```

Evidence:

```text
screenshots/01-vbr01-domain-join-validation.png
```

## Repository validation

Confirmed:

```text
Backup repository host: VBR01.lab.local
Backup repository path: D:\Backup
Repository disk: D: BACKUP_REPO
```

Evidence:

```text
screenshots/02-vbr01-backup-repository-disk.png
screenshots/05-veeam-default-backup-repository.png
```

## FS01 backup validation

Confirmed:

```text
Job: FS01_File_Server_Backup
Type: Windows Agent Backup
Result: Success
Target: Default Backup Repository
```

Evidence:

```text
screenshots/07-veeam-fs01-backup-job-success.png
screenshots/08-veeam-backup-files-created-in-repository.png
```

## Incremental backup validation

Confirmed:

```text
Initial full backup created
Second run created an incremental backup
Backup chain contains metadata, full backup, and incremental backup files
```

Evidence:

```text
screenshots/09-veeam-incremental-backup-created.png
```

## Restore validation

Confirmed:

```text
Test file deleted from FS01
File found inside Veeam backup browser
File restored to original location
File visible again from CLIENT01 mapped drive
```

Evidence:

```text
screenshots/10-restore-test-file-deleted-from-fs01.png
screenshots/11-veeam-backup-browser-restore-test-file-found.png
screenshots/12-restored-file-back-on-fs01.png
screenshots/13-client01-restored-file-visible-in-it-share.png
```

## DC01 backup validation

Confirmed:

```text
DC01 added as a Veeam managed Windows server
Backup mode: Entire computer
Job result: Success
```

Evidence:

```text
screenshots/14-veeam-dc01-managed-server-added.png
screenshots/15-veeam-dc01-entire-computer-backup-mode.png
screenshots/17-veeam-dc01-entire-computer-backup-success.png
```

## Restore scope note

The restore validation was performed for `FS01` file-level recovery.

`DC01` was backed up but not restored in this lab. Domain Controller restore requires a separate controlled Active Directory disaster recovery lab.
