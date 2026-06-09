# Notes

## Why VMware DHCP Was Disabled

Only one DHCP server should serve a subnet. VMware DHCP was disabled on `VMnet8` to avoid conflicts and to make Windows Server responsible for DHCP services.

## Why DHCP Options Matter

DHCP does not only provide an IP address. In this lab, DHCP also provides the client with:

- Default gateway
- DNS servers
- DNS suffix

For Active Directory environments, the DNS option is critical because clients must use domain DNS servers to locate Domain Controllers.

## Why Use a Reservation

A DHCP reservation keeps the endpoint dynamically managed while ensuring it always receives the same IP address.

This is useful for devices that should keep a predictable IP without being configured manually on the endpoint.

## Why Use DHCP Failover

Without DHCP failover, clients depend on a single DHCP server. With Hot Standby failover, the secondary server can continue serving DHCP clients if the active DHCP server becomes unavailable.
