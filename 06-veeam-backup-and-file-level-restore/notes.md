# Notes - Lab 06

## Veeam Backup Server

The Veeam Backup Server is the management component. It stores the configuration database, manages jobs, coordinates backup sessions, and provides the restore console.

In this lab:

```text
VBR01 = Veeam Backup Server
```

## Backup Repository

The backup repository is where backup files are stored.

In this lab:

```text
VBR01 D: drive = BACKUP_REPO
Repository path = D:\Backup
```

## Veeam Proxy / Data Mover

A proxy or data mover component handles backup data movement and processing.

Simple model:

```text
Backup Server = coordinator
Proxy/Data Mover = worker that transfers backup data
Repository = storage location for backup files
```

In this lab, the default components were used. No additional proxy was required.

## Full backup

A full backup is the baseline backup file. It contains the protected data at the time the first backup was created.

Common Veeam full backup file extension:

```text
.vbk
```

## Incremental backup

An incremental backup stores only changes since the previous restore point.

Common Veeam incremental file extension:

```text
.vib
```

Backup chain example:

```text
Full backup
└── Incremental backup 1
    └── Incremental backup 2
```

## Metadata file

The metadata file describes the backup chain and restore points.

Common Veeam metadata file extension:

```text
.vbm
```

## Application-aware processing

Application-aware processing helps create consistent backups by preparing the guest operating system and applications before the backup is taken.

This is especially important for infrastructure servers and application servers.

In this lab:

```text
FS01 = application-aware processing enabled
DC01 = application-aware processing enabled
```

## File-level restore

File-level restore allows restoring individual files or folders without restoring the entire machine.

In this lab, the file-level restore was used to recover:

```text
D:\Shares\IT\restore-test.txt
```

## Domain Controller restore warning

Although DC01 was backed up, it was not restored in this lab.

Domain Controller restore is an advanced disaster recovery process involving Active Directory consistency, SYSVOL, replication, FSMO roles, and authoritative/non-authoritative restore decisions.
