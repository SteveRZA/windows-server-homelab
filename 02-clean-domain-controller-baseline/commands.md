# Commands Used - Lab 02

## DC01 Network Validation

```powershell
ipconfig /all
```

Used to verify the static IP configuration on the domain controller.

Expected DC01 configuration:

```text
IPv4 Address: 192.168.44.10
Default Gateway: 192.168.44.2
DNS Server: 192.168.44.10
DHCP Enabled: No
```

---

## DNS Validation

```powershell
nslookup dc01.lab.local
nslookup google.com
ping google.com
```

Used to confirm both internal AD DNS resolution and external DNS resolution through DNS forwarders.

---

## FSMO Role Validation

```powershell
netdom query fsmo
```

Used to confirm all FSMO roles are hosted on `DC01.lab.local`.

---

## Client Domain Validation

Run on `CLIENT01` after joining the domain:

```powershell
whoami
gpresult /r
nltest /dsgetdc:lab.local
```

Purpose:

- `whoami` confirms the logged-in domain account
- `gpresult /r` confirms Group Policy processing
- `nltest /dsgetdc:lab.local` confirms Domain Controller discovery

---

## Group Policy Refresh

```powershell
gpupdate /force
gpresult /r
```

Used after moving `CLIENT01` into the `LAB/Computers` OU to confirm the updated AD location.

---

## NTP Configuration on DC01

```cmd
w32tm /config /manualpeerlist:"time.windows.com,0x8" /syncfromflags:manual /reliable:yes /update
net stop w32time
net start w32time
w32tm /resync
w32tm /query /status
```

Used to configure the PDC Emulator as a reliable time source and synchronize it with an external NTP source.
