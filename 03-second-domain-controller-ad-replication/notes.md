# Notes - Lab 03

## Lab Purpose

This lab was created to move from a single Domain Controller environment to a more realistic Active Directory design with redundancy.

The focus was not only to add another server, but to understand how Domain Controllers work together through DNS, replication, and service discovery.

## Why DC02 Uses DC01 During Initial Setup

Before `DC02` is promoted, it must use `DC01` as its DNS server so it can locate the existing `lab.local` domain and join it successfully.

After promotion, `DC02` becomes a DNS server itself.

## Why FSMO Roles Stayed on DC01

FSMO roles do not automatically move when a second Domain Controller is added.

In this lab, the expected and intended state is:

```text
All FSMO roles -> DC01.lab.local
```

Future labs can cover FSMO role transfer and seizure scenarios.

## RODC Note

`DC02` was configured as a normal writable Domain Controller, not an RODC.

An RODC is a Read-Only Domain Controller commonly used in branch offices or less trusted physical locations. That was outside the scope of this lab.

## DCDIAG Note

The initial `dcdiag /q` output showed old System Log events. These did not indicate active replication or AD database failure.

The following checks confirmed that the environment was healthy:

- `repadmin /replsummary`
- `repadmin /showrepl`
- `dcdiag /test:ridmanager /v`
- `nslookup dc01.lab.local`
- `nslookup dc02.lab.local`
- `nltest /dsgetdc:lab.local`

After clearing old System Log events, `dcdiag /q` returned no current errors.
