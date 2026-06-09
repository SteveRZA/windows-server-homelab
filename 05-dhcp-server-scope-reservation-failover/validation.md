# Validation

## DHCP Scope

Validated in DHCP console:

- Scope: `LAB-CLIENTS`
- Network: `192.168.44.0/24`
- Range: `192.168.44.100 - 192.168.44.200`

## DHCP Scope Options

Validated options:

- `003 Router`: `192.168.44.2`
- `006 DNS Servers`: `192.168.44.10`, `192.168.44.11`
- `015 DNS Domain Name`: `lab.local`

## Client Lease from DC01

Validated on `CLIENT01`:

- DHCP enabled: `Yes`
- DHCP Server: `192.168.44.10`
- IPv4 Address: `192.168.44.100`
- DNS Servers: `192.168.44.10`, `192.168.44.11`

## Server-side Lease Verification

Validated in DHCP console:

- `CLIENT01.lab.local` received lease `192.168.44.100`

## Reservation

Validated in DHCP console:

- Reservation: `192.168.44.100` for `CLIENT01.lab.local`

## DHCP Failover

Validated on `DC02`:

- Scope replicated to `DC02`
- Failover relationship: `dc01.lab.local-DC02.lab.local`
- State: `Normal`
- Mode: `Hot standby`

## Failover Test

The DHCP service on `DC01` was stopped temporarily.

Validated on `CLIENT01`:

- DHCP Server changed to `192.168.44.11`
- Client still received valid network configuration

This confirmed that `DC02` successfully handled DHCP requests during the failover test.
