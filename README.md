# Windows Server Home Lab

A documented Windows Server lab built from scratch in VMware Workstation, used to design and validate infrastructure before applying it in production. Lab 08 (Windows LAPS) became the basis for a real deployment across ~200 workstations at work.

Every lab is a standalone write-up with the same structure:

| File | Contents |
| --- | --- |
| `README.md` | Full walkthrough: objective, design decisions, configuration, validation |
| `commands.md` | The PowerShell and CLI commands used |
| `notes.md` | Problems hit, why they happened, how they were fixed |
| `validation.md` | How the result was proven to work |
| `screenshots/` | 10–17 screenshots per lab, indexed in `screenshot-index.md` |

## Environment

| Component | Detail |
| --- | --- |
| Hypervisor | VMware Workstation |
| Network | VMware NAT — `192.168.44.0/24` |
| Domain | `lab.local` |
| Server OS | Windows Server 2019 / 2022 Standard (Desktop Experience) |
| Client OS | Windows 11 Pro |

| Host | Role | IP |
| --- | --- | --- |
| `DC01` | Domain Controller, DNS, DHCP primary, FSMO holder, NTP | `192.168.44.10` |
| `DC02` | Additional Domain Controller, DNS, DHCP failover partner | `192.168.44.11` |
| `FS01` | Dedicated file server | `192.168.44.20` |
| `VBR01` | Veeam Backup & Replication server | `192.168.44.30` |
| `CLIENT01` | Domain-joined workstation | DHCP |

## Labs

| # | Lab | What it covers |
| --- | --- | --- |
| 01 | [Initial Active Directory Lab](./01-initial-active-directory-lab) | First `lab.local` build: AD DS, AD-integrated DNS with external forwarding, NTP from the PDC Emulator, SMB shares, NTFS and share permissions, security groups, GPP drive mapping |
| 02 | [Clean Domain Controller Baseline](./02-clean-domain-controller-baseline) | Rebuilt from a fresh install as a structured foundation: OU design, domain users and groups, admin account separation, client domain join, GPO validation, external NTP source |
| 03 | [Second Domain Controller & AD Replication](./03-second-domain-controller-ad-replication) | `DC02` promoted for AD and DNS redundancy; replication validated with `repadmin` and `dcdiag`, FSMO placement confirmed, client DNS redundancy and DC discovery tested |
| 04 | [File Server — NTFS, SMB & GPO Mapped Drives](./04-dedicated-file-server-ntfs-smb-gpo-mapped-drives) | File services moved off the DCs onto `FS01`: separate data disk, SMB shares, NTFS permissions via nested AD groups, GPP drive mapping with item-level targeting, access and denial both verified |
| 05 | [DHCP — Scope, Reservation & Failover](./05-dhcp-server-scope-reservation-failover) | VMware NAT DHCP replaced with Windows DHCP: `LAB-CLIENTS` scope, scope options, client reservation, and Hot Standby failover to `DC02` with a tested failover lease |
| 06 | [Veeam Backup & File-Level Restore](./06-veeam-backup-and-file-level-restore) | Dedicated `VBR01` backup server, repository and managed servers, full and incremental jobs; a file is deleted from `FS01`, restored, and verified from the client. DC backup configured, DC restore deliberately left as a separate scenario |
| 07 | [GPO Workstation Hardening & Account Lockout](./07-gpo-workstation-hardening-and-account-lockout) | Policy scoping done properly: computer hardening on workstation objects, user restrictions on standard users only, lockout policy at domain level. Verified that restrictions hit standard users and not admins |
| 08 | [Windows LAPS Deployment](./08-Windows-LAPS-Deployment-and-Local-Administrator-Password-Management) | Unique rotating local admin passwords stored in AD. Covers why GPP passwords and startup scripts were rejected, the schema extension troubleshooting in a two-DC environment, GPO configuration, retrieval via ADUC and PowerShell, and a verified rotation |

## Why this lab exists

This lab was built primarily to learn. Reading about Active Directory, Group Policy or LAPS is not the same as building them, breaking them, and having to work out why something failed at 11pm on a Sunday.

Each lab started from a question I could not answer confidently from documentation alone — so the write-ups include the mistakes, the errors and the dead ends, not just the working end state. That is the part that taught me the most, and it is the part most write-ups leave out.

The side effect is that the work carried over: the LAPS build in Lab 08 gave me the confidence and the documented procedure to run the same deployment in a live environment.

---

**Stefanos Routsis** — IT Support Technician, Athens
[LinkedIn](https://www.linkedin.com/in/stefanos-routsis-b4a228221/)
