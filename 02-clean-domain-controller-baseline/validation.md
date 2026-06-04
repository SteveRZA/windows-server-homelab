# Validation - Lab 02

## Validation Summary

| Area | Command / Tool | Expected Result | Evidence |
|---|---|---|---|
| DC static IP | `ipconfig /all` | DC01 uses `192.168.44.10` and DNS points to itself | `01-dc01-static-ip-configuration.png` |
| AD DS / DNS roles | Server Manager | AD DS and DNS roles are installed | `02-server-manager-ad-ds-dns-roles.png` |
| Internal DNS | `nslookup dc01.lab.local` | Resolves to `192.168.44.10` | `03-dns-and-fsmo-validation.png` |
| External DNS | `nslookup google.com` / `ping google.com` | External names resolve and respond | `03-dns-and-fsmo-validation.png` |
| FSMO roles | `netdom query fsmo` | All roles point to `DC01.lab.local` | `03-dns-and-fsmo-validation.png` |
| OU structure | ADUC | `LAB` OU contains Users, Computers, Servers, Groups, Admins | `04-ad-ou-structure.png` |
| Security groups | ADUC | Department and admin security groups exist | `05-ad-security-groups.png` |
| Admin account | ADUC | Dedicated `Lab Admin` account exists | `06-ad-admin-account.png` |
| Admin group membership | ADUC | `Lab Admin` is member of `SG_Lab_Admins` | `07-admin-group-membership.png` |
| Domain Admin delegation | ADUC | `SG_Lab_Admins` is member of `Domain Admins` | `08-domain-admins-group-membership.png` |
| Client domain join | Windows Settings | `CLIENT01.lab.local` is shown | `09-client01-domain-joined.png` |
| Domain login | `whoami` | Logged in as `lab\lab.admin` | `10-whoami-domain-login.png` |
| Group Policy source | `gpresult /r` | Group Policy applied from `DC01.lab.local` | `11-gpresult-computer-settings.png` |
| User groups | `gpresult /r` | `lab.admin` is in `SG_Lab_Admins` and `Domain Admins` | `12-gpresult-user-groups.png` |
| DC discovery | `nltest /dsgetdc:lab.local` | Discovers `\\DC01.lab.local` | `13-nltest-dc-discovery.png` |
| Computer OU move | ADUC | `CLIENT01` appears in `LAB/Computers` | `14-client01-moved-to-computers-ou.png` |
| OU path after move | `gpresult /r` | Computer DN shows `OU=Computers,OU=LAB` | `15-client01-gpresult-after-ou-move.png` |
| NTP source | `w32tm /query /status` | Source is `time.windows.com,0x8` | `16-dc01-ntp-external-source.png` |

---

## Final Validation State

The clean domain baseline is functional:

```text
DC01 = Domain Controller / DNS / NTP
CLIENT01 = Joined to lab.local
Domain = lab.local
DNS = Internal and external resolution working
NTP = External sync configured
OU structure = Clean LAB hierarchy created
Admin access = Group-based admin model implemented
```
