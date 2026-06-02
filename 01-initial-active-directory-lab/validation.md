# Validation Checklist

| Check | Expected Result | Screenshot |
|---|---|---|
| DC01 domain membership | DC01 is joined to `lab.local` | `01-dc01-domain-info.png` |
| AD structure | OU and security groups exist | `02-active-directory-structure.png` |
| Share folders | `IT` and `HR` folders exist under `C:\Shares` | `03-shares-folder-structure.png` |
| NTFS permissions | `IT_Shares` has access to `C:\Shares\IT` | `04-it-ntfs-permissions.png` |
| DNS records | DC and client A records exist | `05-dns-zone-records.png` |
| NTP | DC syncs with `time.windows.com,0x8` | `06-ntp-status.png` |
| Drive map GPO | `Z:` maps to `\\DC01\IT` | `07-gpo-drive-map-settings.png` |
| Client mapped drive | `IT Share (Z:)` appears on the client | `08-client-mapped-drive.png` |
| Applied GPO | `Mapped_drive GPO` appears under applied user GPOs | `09-gpresult-applied-gpo.png` |
| Group membership | User is a member of `IT_Shares` | `10-gpresult-user-groups.png` |

## Notes

- `Local Group Policy` appearing as filtered out is normal in this output because it has no applied settings.
- The mapped drive is applied through User Configuration, so validation must be done while logged in as the target domain user.
