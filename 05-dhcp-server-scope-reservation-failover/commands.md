# Commands Used

## CLIENT01 - Renew DHCP Lease

```cmd
ipconfig /release
ipconfig /renew
ipconfig /all
```

## CLIENT01 - DNS and Domain Validation

```cmd
nslookup dc01.lab.local
nslookup dc02.lab.local
nslookup google.com
nltest /dsgetdc:lab.local
```

## DC01 - Stop DHCP Service for Failover Test

```cmd
net stop dhcpserver
```

## DC01 - Start DHCP Service After Failover Test

```cmd
net start dhcpserver
```

## Useful DHCP PowerShell Checks

```powershell
Get-DhcpServerv4Scope
Get-DhcpServerv4OptionValue -ScopeId 192.168.44.0
Get-DhcpServerv4Lease -ScopeId 192.168.44.0
Get-DhcpServerv4Reservation -ScopeId 192.168.44.0
Get-DhcpServerv4Failover
```
